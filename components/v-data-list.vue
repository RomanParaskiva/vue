<template>
  <div :class="list.class">
    <input
      :id="list.id"
      :list="list.listId"
      :name="list.id"
      :placeholder="list.placeholder"
    />

    <datalist :id="list.listId">
      <option
        v-for="option in op"
        :key="option"
        :value="option"
      ></option>
    </datalist>
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
input {
    background: rgba(0, 0, 0, 0.0001);
    border: 2px solid #ffffff;
    font-size: 13px;
    color: #ffffff;
    padding: 10px 12px;
    outline: none;
    display: flex;
    align-items: center;
    border-radius: 4px;
  }
.single {
  margin-right: auto;
}

.twin.left {
    input {
        border-top-right-radius: 0;
        border-bottom-right-radius: 0;
        border-right-width: 0.5px;
    }
}

.twin.right {
    input {
        border-top-left-radius: 0;
        border-bottom-left-radius: 0;
        border-left-width: 0.5px;
    }
}

@media (max-width: 767px) {
  input {
    width: 100%;
    margin-bottom: 8px;
}
.single {
      margin-right: 0;
      width: 100%;
  }
.twin.left {
    input {
        border-top-right-radius: 4px;
        border-bottom-right-radius: 4px;
        border-right-width: 2px;
    }
}

.twin.right {
    input {
        border-top-left-radius: 4px;
        border-bottom-left-radius: 4px;
        border-left-width: 2px;
    }
  }
}
</style>
