<template>


  <div class="app">

    <h1>Todo List</h1>
    
      <table class="add">
        <tr>

          <td class="tdnew">
            <input type="text" todo="todo" v-model="newTodo" />
          </td>

          <td class="tdadd">
            <button class="addbt" @click="insertContact">Add</button>
          </td>

        </tr>
      </table>

        
      
   
      <table class="list">

        <tr v-for="item in contactLists" :key="item.id">

          <td class="listtext">
            <input class="todolist" type="text" v-model="item.todo" />
          </td>

          <td class="udbtn">
            <button class="upbt" @click="updateContact(item.id, item.todo)">Update</button>
          </td>

          <td class="udbtn">
            <button class="debt" @click="deleteContact(item.id)">Delete</button>
          </td>
        </tr>
      </table>
    
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      newTodo: "",
      contactLists: [],
    };
  },
  methods: {
    async getContact() {
      const resData = await axios.get("base64:PjB+WR98TlcDh9MMC2hWs8c92vIvPsdXjJzG9g3WgOg=");
      this.contactLists = resData.data.data;
    },
    async insertContact() {
      const sendData = {
        todo: this.newTodo
      };
      await axios.post("base64:PjB+WR98TlcDh9MMC2hWs8c92vIvPsdXjJzG9g3WgOg=", sendData);
      await this.getContact();
    },
    async updateContact(id, todo) {
      const sendData = {
        todo: todo
      };
      await axios.put("base64:PjB+WR98TlcDh9MMC2hWs8c92vIvPsdXjJzG9g3WgOg=" + id, sendData);
      await this.getContact();
    },
    async deleteContact(id) {
      await axios.delete("base64:PjB+WR98TlcDh9MMC2hWs8c92vIvPsdXjJzG9g3WgOg=" + id);
      await this.getContact();
    },
  },
  created() {
    this.getContact();
  },
};
</script>

<style>


h1{
   font-family: 'Sacramento', cursive;
}


/*全体背景 */
body{ 
  background-color: lightblue;
}

/*全体要素(枠、背景など) */
.app{
  background-color: linen;
  padding: 20px 10% 50px 10%;
  margin: 130px auto;
  border: solid 3px gray;
  border-radius: 10px;
  width: 60%;
}

/*それぞれの表(入力テキスト、Addボタン),(追加済みリスト,Update,Deleteボタン) */
table.add,table.list{
  padding: 10px 0;
  width: 100%;
}

/*Todo追加テキスト セル */
.tdnew{
  width: 70%;
}

/*Todo追加ボタン セル */
.tbadd{
  width: 90%;
}

/*Todo一覧テキスト セル */
.listtext{
  width: 60%;
}

/*Todo更新,削除ボタン セル */
.udbtn{
  width: 20%;
}



/*入力要素の全体設定 */
input{
  width: 80%;
  height: 20px;
  margin: 0px 10px;
  padding: 2px;
  border-radius: 3px; 
}


/*ボタンの全体設定 */
button{
  background-color: white;
  padding: 5px auto; 
  font-size: 15px;
  text-decoration: none;
  border-radius: 3px; 
  border:solid 3px ;
  transition: 0.2s ease; /* スタイルが変化する時間 */
}


/*追加ボタン */
.addbt{
  width: 90%;
  color: blue;
}

button.addbt:hover {
  color: white;
  background: blue;
  border-color: blue;
}

/*更新ボタン */
.upbt{
  width: 90%;
  color: crimson;
}

button.upbt:hover {
  color: white;
  background: crimson;
  border-color: crimson;
}

/*削除ボタン */
.debt{
  width: 90%;
  color: black;
}

button.debt:hover {
  color: white;
  background: black;
  border-color: black;
}









</style>