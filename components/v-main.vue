<template>
  <div>
    <div class="main__wrapper">
      <div class="container">
        <h1>
          <div><span>Netwrix </span> <span>Partner Locator</span></div>
        </h1>
        <p>
          Hundreds of Netwrix partners around the world are standing by to help
          you.<br />
          With our Partner Locator you can easily find the list of authorized
          partners in your area.
        </p>

        <div class="input__wrapper">
          <input
            id="search"
            type="text"
            name="search"
            placeholder="Search by company name or adress.."
            autocomplete="off"
            @input="handleInput($event)"
          />
          <span>
            <img src="~/assets/img/search-ico.svg" alt="search" srcset="" />
          </span>
        </div>

        <div class="selects__wrapper">
          <vDataList :init-list="typeList" :options="types" @selectType="handleChange($event)"/>
          <vDataList :init-list="countryList" @selectType="handleChange($event)"/>
          <vDataList :init-list="stateList" @selectType="handleChange($event)"/>
        </div>
      </div>
    </div>
    <div v-if="!loading">
      <div class="partners-list">
        <transition-group name="list" tag="p" appear>
          <v-single-partner
            v-for="partner in filterPartners"
            :key="partner.id"
            :init-partner="partner"
          />
        </transition-group>
      </div>
      <div v-show="emptySearch" style="text-align:center;">
        Your search parameters did not match any partners. Please try different
        search.
      </div>
    </div>
    <transition-group v-else class="load-message" appear>
      <p key="load">Please wait...</p>
    </transition-group>
  </div>
</template>

<script>
import vDataList from './v-data-list.vue'
import VSinglePartner from './v-single-partner.vue'
export default {
  components: { vDataList, VSinglePartner },
  data () {
    return {
      typeList: {
        id: 'type-select',
        listId: 'type-list',
        placeholder: 'Type',
        class: 'single'
      },
      countryList: {
        id: 'country-select',
        listId: 'country-list',
        placeholder: 'Country',
        options: ['USA', 'RU'],
        class: 'twin left'
      },
      stateList: {
        id: 'state-select',
        listId: 'state-list',
        placeholder: 'State',
        options: ['Nairobi', 'Ottawa'],
        class: 'twin right'
      },
      loading: false,
      types: [],
      partners: [],
      filterPartners: [],
      emptySearch: false
    }
  },
  async fetch () {
    this.loading = true
    const { data } = await this.$axios.get('/api/', {
      headers: { 'Content-Type': 'application/json' },
      params: { action: 'getData' }
    })
    if (data.message === 'OK') {
      this.partners = data.res
      this.partners.forEach((p) => {
        p.hidden = true
        if (!this.types.includes(p.status)) {
          this.types.push(p.status)
        }
      })
      this.filterPartners = [...new Set(this.partners)]
      this.loading = false
    }
  },
  methods: {
    handleInput (e) {
      this.filterPartners = [...new Set(this.partners)]
      this.emptySearch = false
      if (e.target.value.length > 1) {
        this.filterPartners = this.partners.filter((item) => {
          return item.company.toLowerCase().includes(e.target.value.toLowerCase()) || item.address.toLowerCase().includes(e.target.value.toLowerCase())
        })
        this.filterPartners.length === 0 ? this.emptySearch = true : this.emptySearch = false
      } else {
        this.filterPartners = [...new Set(this.partners)]
      }
    },
    handleChange (e) {
      console.log(e.target.value)
      this.emptySearch = false
      if (e.target.value !== 'Type') {
        this.filterPartners = [...new Set(this.partners)]
        this.filterPartners = this.partners.filter((item) => {
          return item.status.toLowerCase().includes(e.target.value.toLowerCase())
        })
        this.filterPartners.length === 0 ? this.emptySearch = true : this.emptySearch = false
      } else {
        this.filterPartners = [...new Set(this.partners)]
      }
    }
  }
}
</script>

<style lang="scss">
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.main__wrapper {
  width: 100%;
  height: auto;
  background-image: url("~/assets/img/bg.png");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 120px 0;

  .container {
    width: 100%;
    max-width: 700px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;

    h1 {
      font-weight: 700;
      font-size: 46px;
      line-height: 28px;
      color: #ffffff;
      margin-bottom: 20px;
      & > div {
        display: flex;
        span:first-child {
          margin-right: 10px;
        }
      }
    }

    p {
      font-size: 16px;
      line-height: 32px;
      color: #ffffff;
      margin-bottom: 50px;
    }
    .input__wrapper {
      display: flex;
      position: relative;
      width: 100%;
      padding: 0 30px;
      margin-bottom: 20px;

      input {
        background: #ffffff;
        border: 1px solid #ffffff;
        border-radius: 4px;
        width: 100%;
        font-size: 15px;
        line-height: 32px;
        color: #7f8893;
        padding: 6.5px 16px;
        outline: none;
      }

      & > span {
        position: absolute;
        display: flex;
        align-items: center;
        right: 45px;
        height: 100%;
      }
    }

    .selects__wrapper {
      display: flex;
      width: 100%;
      padding: 0 30px;
    }
  }
}

.partners-list {
  padding: 50px 2rem;
}

.load-message {
  width: 100%;
  display: flex;

  p {
    margin: 20px auto;
    font-size: 20px;
    font-weight: 700;
  }
}

@media (max-width: 767px) {
  .main__wrapper {
    padding: 50px;
    .container {
      max-width: 300px;

      h1 {
        font-size: 30px;
        line-height: 40px;

        & > div {
          flex-direction: column;
        }
      }

      p {
        font-size: 14px;
        line-height: 28px;
      }
    }
  }
  .selects__wrapper {
    flex-direction: column;
  }
}
</style>
