<template>
  <div :class="list.class">
    <select
      :id="list.id"
      :name="list.id"
      @change="$emit('selectType', $event)"
    >
      <option>{{ list.placeholder }}</option>
      <option
        v-for="option in op"
        :key="option"
        :value="option"
      >{{ option }}</option>
    </select>
  </div>
</template>

<script>
export default {
  props: { initList: Object, options: Array },
  data () {
    return {
      list: this.initList,
      op: this.options
    }
  }
}
</script>

<style lang="scss" scoped>
select {
    background: rgba(0, 0, 0, 0.0001);
    border: 2px solid #ffffff;
    font-size: 13px;
    color: #ffffff;
    padding: 10px 12px;
    outline: none;
    display: flex;
    align-items: center;
    border-radius: 4px;
    min-width: 210px;

    &:focus {
      outline: 0.15em solid #00f;
      box-shadow: 0 0 0.2em #00f;
    }

    option {
      color: #354556;
    }
  }

 select::-ms-expand {
      margin-right: 10px;
    }
.single {
  margin-right: auto;
}

.twin.left {
    select {
        border-top-right-radius: 0;
        border-bottom-right-radius: 0;
        border-right-width: 0.5px;
    }
}

.twin.right {
    select {
        border-top-left-radius: 0;
        border-bottom-left-radius: 0;
        border-left-width: 0.5px;
    }
}

@media (max-width: 767px) {
  select {
    width: 100%;
    margin-bottom: 8px;
}
.single {
      margin-right: 0;
      width: 100%;
  }
.twin.left {
    select {
        border-top-right-radius: 4px;
        border-bottom-right-radius: 4px;
        border-right-width: 2px;
    }
}

.twin.right {
    select {
        border-top-left-radius: 4px;
        border-bottom-left-radius: 4px;
        border-left-width: 2px;
    }
  }
}
</style>
