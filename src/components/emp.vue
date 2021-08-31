<template>
  <div>
    <div class="data">
      <table>
        <tr>
          <td>ID</td>
          <td>Name</td>
          <td>Email</td>
          <td>Avtar</td>
        </tr>
        <tr v-for="item in entries" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.first_name }}</td>
          <td>{{ item.email }}</td>
          <td><img v-bind:src="item.avatar" alt="" /></td>
        </tr>
      </table>
      <br />
     
    </div>
    <div class="pages_section">
      <div class="pages"  v-for="item in total" :key="item" v-on:click="get({item})">{{ item }}</div>
    </div>
  </div>
</template>
<script>
export default {
  name: "emp",
  data() {
    return {
      entries: [],
      total: [],
    };
  },
  created() {
      document.title = "EMP";
    this.getemployeedata().then((res) => {
      this.entries = res.data;
      this.total = res.per_page;
      console.log(res);
    });
  },
  methods: {
      
    async getemployeedata() {
      const response = await fetch("https://reqres.in/api/users?page=2");
      return response.json();
    },

    test() {
      console.log(this.entries[0].id);
    },
    get(i)
    {
       
        fetch(`https://reqres.in/api/users?page=${i.item}`)
        .then((res) => res.json())
        .then((res) =>{ console.log(res);
                this.entries = res.data;
               
                this.total = res.per_page;
                   if(this.entries.length == 0){alert("No Data on this Page");
              }
        
        }
        );
        
        
            
    }
  },
};
</script>

<style >
td {
  width: 250px;
  height: 50px;
}
.pages_section {
  margin: 15px 0 0 0;
  display: flex;
  justify-content: center;
  align-items: center;

}
.pages {
  padding: 15px 0 0 0;
  margin: 0 5px 0 5px;
  text-align: center;
  width: 50px;
  height: 50px;
  border: 1px solid crimson;
  cursor: pointer;
}

table {
  margin: 0 auto 0 auto;
}
</style>