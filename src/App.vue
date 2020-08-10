<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <appTodolist :ToDoList="ToDoList" :ToDoListShow="ToDoListShow" />
    <div id="loading" class="loading">
      <img src="./image/loading.jpg" alt="loading..." />
    </div>
  </div>
</template>

<script>
import Axios from "axios";
import appTodolist from "@/components/app-todolist";

export default {
  name: "App",
  data() {
    return {
      title: "ToDo List",
      ToDoList: null,
      ToDoListShow: false,
    };
  },
  components: {
    appTodolist,
  },
  mounted: function() {
    Axios.get("https://jsonplaceholder.typicode.com/users/1/todos")
      .then((response) => response.data)
      .then((data) => (this.ToDoList = data));
    document.getElementById("loading").style.display = "none";
  },
};
</script>

<style lang="scss">
@import url("./scss/main.scss");
*,
body,
html {
  font-family: "Poppins", sans-serif;
}
body {
  background: linear-gradient(150deg, #5c47ad, #b070ce);
  color: #fff;
}
#app {
  border-radius: 18px;
  width: 310px;
  margin: 20px auto;
  box-shadow: 0px 8px 50px rgba($color: #000000, $alpha: 0.3);
  background: #070619;
  h1 {
    width: 100%;
    text-align: center;
    font-size: 24px;
    font-weight: bold;
    padding: 10px 0;
  }
  .newTask {
    width: 100%;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    input {
      width: 100%;
      background: transparent;
      border: none;
      padding: 10px 5px;
      font-size: 18px;
      border-top: 1px solid #000;
      border-bottom: 1px solid #000;
    }
    input:focus {
      outline: none;
    }
    button {
      width: 50%;
      padding: 10px 5px;
      border: none;
      background-color: transparent;
      border-radius: 5px;
      color: #000;
      transition: color 0.5s;
      cursor: pointer;
      font-size: 18px;
      font-weight: 500;
    }
    button:focus,
    button:hover {
      outline: none;
    }
    button[name="add"]:hover {
      color: #00dd00;
    }
    button[name="clear"]:hover {
      color: #dd0000;
    }
  }
  .pageTab {
    width: 100%;
    display: flex;
    align-items: center;
    z-index: 2;
    p {
      width: 50%;
      height: 10%;
      background-color: #e7e9f8;
      border-radius: 18px 18px 0 0;
      color: #000;
      font-weight: bold;
      font-size: 16px;
      cursor: pointer;
      opacity: 1;
      text-align: center;
      padding: 10px 0;
    }
    p:nth-child(1) {
      border-radius: 18px 0 0 0;
    }
    p:nth-child(2) {
      border-radius: 0 18px 0 0;
    }
    .not_active {
      background: linear-gradient(to top, #e7e9f8 5%, #777788 95%);
    }
  }
  ul {
    border-radius: 0 0 18px 18px;
    background-color: #e7e9f8;
    padding: 10px 20px;
    height: 520px;
    display: flex;
    flex-direction: column;
    li:nth-child(1) {
      height: 456px;
      width: 100%;
      display: flex;
      flex-direction: column;
      flex-wrap: wrap;
      overflow-x: hidden;
      .pageTask {
        transition: left 0.3s ease;
        position: relative;
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 18px;
        padding: 15px;
        font-weight: 600;
        background: linear-gradient(150deg, #f0618f, #6c65bf);
        border-radius: 12px;
        margin-bottom: 22px;
        margin-right: 20px;
        box-shadow: 0px 3px 2px rgba($color: #000000, $alpha: 0.3);
        cursor: pointer;
        user-select: none;
        p {
          max-width: 200px;
          min-height: 100px;
        }
        ion-icon {
          font-size: 40px;
        }
      }
    }
    .pageButton {
      flex: 1 1 auto;
      width: 100%;
      display: flex;
      align-items: flex-end;
      justify-content: space-between;
      button {
        width: 49%;
        border-radius: 12px;
        border: 0;
        text-transform: uppercase;
        background: linear-gradient(150deg, #f0618f, #6c65bf);
        cursor: pointer;
        ion-icon {
          color: #fff;
          font-size: 30px;
        }
      }
      button:focus {
        outline: 0;
      }
      button:hover {
        filter: brightness(1.1);
      }
    }
  }
  .loading {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #000;
    img {
      animation: loading 3s infinite linear;
      transform: rotateZ(0deg);
      width: 150px;
      height: auto;
    }
  }
}

@keyframes loading {
  0% {
    transform: rotateZ(0deg);
  }
  100% {
    transform: rotateZ(360deg);
  }
}
</style>
