<template>
  <div
      class="contain"
      :class="{'disabled': isDisabled}"
  >
    <input
        @change="dis"
        :checked="isDisabled"
        type="checkbox"
        name="check"
        id="check"
    />
    <div
        class="content"
    >
      <p>{{ text }}</p>
      <span
          @click="remove"
          class="material-icons span i"
      >delete</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Item',
  props: {
    text: {
      type: String,
      required: true
    },
    isDisabled: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    remove: function (e) {
      this.$emit('deleting', e.target.previousElementSibling.textContent)
    },
    dis: function (e) {
      e.target.parentElement.classList.toggle('disabled')
      this.$emit('disable', e.target.nextElementSibling.firstElementChild.textContent)
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

  .contain {
    display: flex;
    background: #bdd6ee;
    color: #262626;
    justify-content: space-between;
    align-items: center;
    width: 600px;
    margin-bottom: 10px;
    padding: 15px;
    box-shadow: 0 0 0;
    transition: box-shadow .2s linear;
  }

  .contain:hover {
    background: #95c2ec;
    box-shadow: 2px 4px 25px -14px rgba(0,0,0,0.55);
  }

  .content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
  }

  p {
    margin-left: 20px;
    font-size: 1.5rem;
    font-family: 'Montserrat';
  }

  span {
    margin-right: 20px;
    cursor: pointer;
    color: #949494;
  }

  span:hover {
    color: #262626;
  }

  span:active {
    color: #b00505;
  }

  input {
    display: block;
  }

  .disabled {
    background: #ccc;
    color: darkgray;
  }

  .disabled:hover {
    background: #ccc;
    box-shadow: 0 0 0;
  }
</style>
