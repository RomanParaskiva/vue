<template>
    <div v-show="partner.hidden" class="conatainer partner" :key="partner.id">
      <div class="partner__logo">
        <img :src="partner.logo" alt="logo" />
      </div>
      <div class="partner__credits">
        <h4>{{ partner.company }}</h4>
        <p>{{ partner.address }}</p>
      </div>
      <div class="partner__contacts">
        <a class="link" href="partner.website">Website</a>
        <a class="phone-link" :href="'tel:+' + partner.phone">{{
          partner.phone
        }}</a>
      </div>
      <div class="partner__type">
        <div class="divider"></div>
        <span id="partner-type">{{ partner.status }}</span>
      </div>
    </div>
</template>

<script>
export default {
  props: { initPartner: { type: Object, default: () => {} } },
  data () {
    return {
      partner: this.initPartner
    }
  }
}
</script>

<style lang="scss">
.partner {
  display: grid;
  grid-template-columns: 1fr 3fr 1fr 1fr;
  width: 100%;
  max-width: 1260px;
  background: #ffffff;
  box-shadow: 0px 1px 2px rgba(5, 27, 43, 0.14);
  padding: 35px 40px;
  border-radius: 4px;
  margin: 0 auto 20px;

  .partner__logo {
    margin-right: 70px;
    margin-bottom: auto;
  }

  .partner__credits {
    margin-bottom: auto;
    width: 100%;
    max-width: 390px;
    margin-bottom: 10px;

    h4 {
      font-size: 21px;
      line-height: 32px;
      color: #354556;
      margin-bottom: 13px;
    }

    p {
      font-size: 14px;
      line-height: 24px;
      color: #354556;
    }
  }

  .partner__contacts {
    display: flex;
    flex-direction: column;
    margin-left: auto;
    margin-bottom: auto;
    width: 100%;

    .link {
      font-size: 14px;
      line-height: 32px;
      color: #0068da;
      position: relative;
      text-decoration: none;
      display: block;
      width: max-content;

      &::after{
          content: '';
          display: block;
          position: absolute;
          bottom: 5px;
          width: 100%;
          height: 1px;
          background-color: #0068da;
          opacity: .3;
      }

    }

    .phone-link {
      font-size: 13px;
      line-height: 32px;
      color: #354556;
      text-decoration: none;
    }
  }

  .divider {
    width: 1px;
    height: 58px;
    background: #dcdee0;
    margin-right: 48px;
  }

  .partner__type {
    display: flex;
    width: 100%;
    padding-left: 20px;
    margin-bottom: auto;
    height: 100%;
    align-items: center;
    font-weight: 600;
    font-size: 13px;
    line-height: 32px;
    color: #354556;

    span {
      margin-bottom: auto;
    }
  }
}

@media (max-width: 767px) {
    .partner{
        display: flex;
        flex-direction: column;
        width: 100%;
        max-width: 300px;
        padding: 30px 24px;

        .partner__logo {
            margin-bottom: 40px;
        }

        .partner__credits {
            border-bottom: 1px solid #DCDEE0;
            padding-bottom: 28px;
            h4 {
                margin-bottom: 14px;
            }
        }
        .partner__type{
            padding-left: 0;
            .divider {
                display: none;
            }
        }
    }
}
</style>
