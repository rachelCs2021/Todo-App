<template>
<form @submit="onSubmit" class="add-form">
  <i @click="onClick" class="fas fa-times"></i>
    <div class="form-control">
        <label for="title">כותרת</label>
        <input type="text" v-model="title" name="title" placeholder="כותרת" id="title" >
    </div>
    <div class="form-control">
        <label for="description">תאור</label>
        <input type="text" v-model="description" name="description" placeholder="תאור המטלה" id="description" >
    </div>
    <div class="form-control">
        <label for="date">תאריך דדליין</label>
        <input type="text" v-model="date" name="date" placeholder="תאריך & יום" id="date" >
    </div>
    <div class="form-control">
        <label for="priority">עדיפות</label>
        <div class="priority">

           <input type="radio" value="high" v-model="choose" name="choose" id="high"  >
           <label for="high" class="choose high">גבוהה</label>

           <input type="radio" value="medium" v-model="choose" name="choose" id="medium" >
           <label for="medium" class="choose medium">רגילה</label>

           <input type="radio" value="low" v-model="choose" name="choose" id="low" >
           <label for="low" class="choose low" >נמוכה</label>
        </div>
    </div>
    <div class="form-control"> 
        
     <label for="repeat">חזרה</label>
      <select class="select" v-model="repeat">
        <option>חד פעמי</option>
           <option>מדי יום</option>
           <option>מדי שבוע</option>
           <option>מדי חודש</option>
           <option>מדי שנה</option>
     </select>
    </div>
        <input type="submit" value="שמור מטלה" class="btn btn-block" >
  </form>
</template>

<script>

export default ({
  name: 'NewTodo',
  data(){
      return {
          title: '',
          description: '',
          date: '',
          priority: '',
          repeat: ''
      }
  },
   methods: {
        onClick() {
            console.log("clicked");
           this.$emit('btn-click')
       },
       onSubmit(e) {
           e.preventDefault()

           if(!this.title || !this.description || !this.date || this.priority || !this.repeat) {
               alert("בבקשה מלאו את כל הפרטים :)")
               return
           }

      const newTodo = {
        //   id: Math.floor(Math.random() * 10000 ), 
          title: this.title,
          description: this.description,
          date: this.date,
          priority: this.choose,
          repeat: this.repeat
      }

      this.$emit('add-todo', newTodo);
      console.log(newTodo);

      this.title = ''
      this.description = ''
      this.date = ''
      this.priority = ''
      this.repeat = ''
       }
   }
})
</script>

<style scoped>

  .add-form{
    background-color: #fff;
    padding: 15px 20px;
    width: 70%;
    margin: auto;
    margin-bottom: 40px;
    margin-top: 10px;
  }

  .fas{
      display: flex;
  }

  .form-control {
     display: flex;
     flex-direction: column;
     padding: 5px 10px;
     margin: 10px 0;
     justify-content: right;
  }

  input[type="text"] {
     width: 97%;
     padding: 5px 10px;
     border-radius: 5px;
     font-size: 15px;
  }

  label{
      text-align: right;
      font-size: 17px;
  }

  .priority{
      display: flex;
  }

  .choose {
       margin: 0 5px 0 15px;
  }

  .select{
      width: 20%;
      padding: 5px;
      border-radius: 5px;
  }

   .high{
     color: red;
  }

  .medium{
      color: black;
  }

  .low{
      color: rgb(205, 50, 200);
  }

   .btn.btn-block {
    background-color: #000000;
    color: #ffffff;
    width: 100%;
    padding: 7px 10px;
    font-size: 17px;
 }
</style>