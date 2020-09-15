<template>
  <div class="container">
    <div class="input__form">
      <input
          placeholder="Hit ENTER to add task..."
          v-model="newTask"
          type="text"
          name="text"
          id="text"
          @keydown.enter="add"
      />
    </div>
    <div class="list">
      <app-list-item
          @deleting="del($event)"
          @disable="makeDisabled"
          v-for="(item, index) in array"
          :text="item.info"
          :key="index"
          :is-disabled="item.isDisabled"
      />
    </div>
  </div>
</template>

<script>
import Item from '@/components/Item'

export default {
  name: 'App',
  data() {
    return {
      newTask: '',
      array: JSON.parse(localStorage.getItem('arr')) || []
    }
  },
  methods: {
    add: function () {
      if( this.newTask.trim() === '' ) return
      this.array.push({
        info: this.newTask.trim(),
        isDisabled: false
      })
      this.newTask = ''
      localStorage.setItem('arr', JSON.stringify(this.array))
    },
    makeDisabled: function (e) {
      this.iterateArray(el => {
        if (e === el.info) {
          el.isDisabled = !el.isDisabled
        }
      })
    },
    del: function (e) {
      this.iterateArray((el, index) => {
        if (e === el.info) {
          this.array.splice(index, 1)
        }
      })
    },
    iterateArray: function (callback) {
      this.array.forEach(callback)
      localStorage.setItem('arr', JSON.stringify(this.array))
    }
  },
  components: {
    'app-list-item': Item,
  }
}
</script>

<style scoped>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }


@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500&display=swap');

  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .input__form {
    margin-bottom: 20px;
    width: 600px;
  }

  input {
    width: 400px;
    height: 50px;
    font-family: 'Montserrat';
    font-size: 1.5rem;
    width: 100% ;
    padding: 15px 30px;
    border: none;
    border-bottom: 3px solid #949494;

  }

  input:hover, input:focus {
    outline: none;
    border-bottom: 3px solid #262626;
  }

  button {
    width: 400px;
    height: 50px;
    font-family: 'Montserrat';
    border-radius: 10px;
    font-size: 1.5rem;
    width: 19%;
    background-color: #4c0b94;
    color: white;
  }
</style>
