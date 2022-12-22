<template>
  <!-- new task form -->
  <form  @submit="onSubmit" class="add-form">
    <div class="form-control">
      <input type="text" v-model="text" name="text" placeholder="Add Task"
      />
    </div>
    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<script>

export default {
  name: "AddTask",
  data() {
    return { 
        text: "", 
        createdAt: new Date(),
        completed: false,
};
  },
  methods: {
    // prevent page reload on submit & add black task
    onSubmit(e) {
      e.preventDefault();
      if (!this.text) {
        alert("Please add a task");
        return;
        
      }

      const newTask = {
        id: Math.floor(Math.random() * 10000),
        description: this.text,
        createdAt: new Date(),
        completed: false,
      };
      console.log(newTask);
      
      this.$emit("add-task", newTask);

      this.description = "",
      this.createdAt= new Date(),
      this.completed = false;
    },
  },
};
</script>

<style lang="scss">

.add-form {
  margin-bottom: 40px;
}

.form-control{
    width: 100%;
    input{
        box-sizing: border-box;
        font-size: 17px;
        background-color: rgba(246, 255, 247, 0.7);
        border-radius: 7px;
        border: 2px solid rgba(0, 0, 0, 0.568);
        padding: 3px 10px 3px 8px;
        width: 100%;
        height: 40px;
    }
}

.btn {
  display: inline-block;
  background: rgb(39, 39, 39);
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin-top: 8px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 17px;
  font-family: inherit;
  :focus {
    outline: none;
  }
  :active {
    transform: scale(0.98);
  }
}

.btn-block {
  display: block;
  width: 100%;
}


</style>
