<template>
  <div id="app">

    <div class="SignIn">
      <button>Login with Github</button>
    </div>

    <div class="todo">
      <div class="todo__header">
        <h4>Task list</h4>
        <span class="HasEntered">
          <img src="./assets/cat.jpg" alt="user">
          User name
          <div class="todo__header-logout">
            <button>LogOut</button>
          </div>
        </span>
      </div>

      <TaskField @onAddTask="onAddTask"/>

      <div class="todo__list">

        <ListItem 
          v-for="(task, index) in tasks"
          :key="index"
          :index="index"
          :text="task.text"
          :completed="task.completed"
          @onToggleCompleted="onToggleCompleted"
          @onRemoveTask="onRemoveTask"
          />

      </div>
    </div>
  </div>
</template>

<script>
import ListItem from '@/components/ListItem.vue'
import TaskField from '@/components/TaskField.vue'

export default {
  name: 'App',
  data: () => ({
    tasks: [
      {
        text: 'Learn VueJs',
        completed: false
      },
      {
        text: 'Learn English',
        completed: false
      }
    ]
  }),
  methods: {
    onToggleCompleted(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    onRemoveTask(index) {
      this.tasks.splice(index, 1)
    },
    onAddTask(text) {
      this.tasks.push({
        text,
        completed: false
      })
    }
  },
  components: {
    ListItem,
    TaskField
  }
}
</script>

<style lang="scss">
* {
  margin: 0px;
  padding: 0px;
  font-family: 'Rubik', sans-serif;
  box-sizing: border-box;
}
body {
  background: #FBFAFB;
}

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 0 15px;
}

.SignIn {
  width: 600px;
  background-color: #fff;
  border: 1px solid #ebebeb;
  box-shadow: 0px 9px 24px rgba(#000000, .01);
  border-radius: 8px;
  padding: 20px;

  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  button {
    width: 200px;
    background-color: #3793E4;
    box-shadow: 0 5px 10px rgba(44,116,255,.2);
    border-radius: 6px;
    border: 0;
    outline: 0;
    color: #fff;
    padding: 0 25px;
    height: 45px;
    font-size: 16px;
    letter-spacing: .5px;
    cursor: pointer;

    &:hover {
      background-color: #318cdb;
      box-shadow: 0 6px 10px rgba(44,116,255,.3);
    }
  }
}

.todo {
  max-width: 600px;
  width: 100%;
  height: 500px;
  background-color: #fff;
  box-shadow: 0px 9px 24px rgba(#000000, .01);
  border-radius: 8px;
  overflow: hidden;
  border: 1px solid #ebebeb;

  &__header {
    background-color: #3793E4;
    padding: 13px 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;

    h4 {
      color: #fff;
      font-size: 22px;
      font-weight: 500;
    }

    span {
      color: #fff;
      font-weight: 500;
      display: flex;
      align-items: center;
      cursor: pointer;
      padding: 7px 12px;
      border-radius: 8px;
      transition: .1s ease;
      position: relative;

      &:hover {
        background-color:  lighten(#3793E4, 8);
      }

      img {
        width: 24px;
        height: 24px;
        object-fit: cover;
        margin-right: 10px;
        border-radius: 50%;
      }

      .todo__header-logout {
        position: absolute;
        bottom: -100%;
        right: 0px;
        width: 100%;
        background-color: #fff;
        padding: 5px;
        box-shadow: 0px 10px 24px rgba(#000000, .1);
        border-radius: 8px;
        display: flex;
        justify-content: center;

        display: none;

        button {
          width: 100%;
          padding: 5px 0;
          background-color: #fff;
          border: 0;
          outline: 0;
          border-radius: 8px;
          cursor: pointer;

          &:hover {
            background-color: darken($color: #fff, $amount: 8);
          } 
        }
      }
    }
  }

  &__add-field {
    display: flex;
    border-bottom: 1px solid #f4f4f4;
    background-color: #fff;

    input {
      border: 0;
      outline: 0;
      font-size: 16px;
      padding: 20px;
      flex: 1;
      background-color: #fff;

      &::placeholder {
        color: #bfbfbf;
      }
    }

    &-button {
      border: 0;
      background-color: #fff;
      width: 65px;
      height: 65px;
      cursor: pointer;

      &:hover {
        background-color: #fbfbfb;

        svg {
          path {
            fill: #202020;
          }
        }
      }
    }
  }

  &__list {
    overflow: auto;
    height: calc(100% - 130px);

    &::-webkit-scrollbar {
      width: 5px;
    }

    &::-webkit-scrollbar-thumb {
      background: #888;
    }

    &-item {
      $self: &;
      display: flex;
      padding: 20px;
      border: 1px solid #f4f4f4;

      &--completed {
        text-decoration: line-through;
        #{$self}-check {
          svg {
            display: block;
          }
        }

        #{$self}-check,
        #{$self}-check:hover {
          background-color: #3793E4;
        }
      }

      &-check {
        display: flex;
        align-items: center;
        justify-content: center;
        border: 2px solid #3793E4;
        border-radius: 30px;
        width: 24px;
        height: 24px;
        margin-right: 15px;
        cursor: pointer;

        svg {
          display: none;
        }        

        &:hover {
          background-color: #d9e3eb;
        }
      }

      &-remove {
        cursor: pointer;
      }

      &-remove:hover {
        svg {
          path {
            fill: #202020;
          }
        }
      }

      p {
        font-size: 18px;
        flex: 1;
      }
    }
  }
}
</style>
