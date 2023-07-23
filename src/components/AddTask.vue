<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label for="task">Task</label
      ><input type="text" v-model="text" name="task" placeholder="Add task" />
    </div>
    <div class="form-control">
      <label for="date-time">Day & Time</label
      ><input
        v-model="day"
        type="datetime-local"
        id="datetime"
        name="date-time"
      />
    </div>
    <div class="form-control form-control-check">
      <label for="set-reminder">Set reminder</label
      ><input v-model="reminder" type="checkbox" name="set-reminder" />
    </div>
    <input type="submit" value="Save task" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return { text: "", day: "", reminder: false };
  },
  methods: {
    parseDate(val) {
      let d = val.split("T")[0];
      let t = val.split("T")[1];
      const months = [
        "Jan",
        "Feb",
        "March",
        "April",
        "May",
        "June",
        "July",
        "Aug",
        "Sept",
        "Oct",
        "Nov",
        "Dec",
      ];

      let monthNum = parseInt(d.split("-")[1]);

      let day = parseInt(d.split("-")[2]);
      let dayStr = "";
      switch (day % 10) {
        case 1:
          dayStr = day + "st";
          break;
        case 2:
          dayStr = day + "nd";
          break;
        case 3:
          dayStr = day + "rd";
          break;
        default:
          dayStr = day + "th";
          break;
      }
      let month = months[monthNum - 1];

      let militaryHour = parseInt(t.split(":")[0]);
      let mins = t.split(":")[1];
      let hourStr = "";
      if (militaryHour === 0) {
        hourStr = 12 + ":" + mins + "am";
      } else if (militaryHour > 12) {
        hourStr = militaryHour - 12 + ":" + mins + "pm";
      } else {
        let str = militaryHour + ":" + mins;
        if (militaryHour === 12) {
          hourStr = str + "pm";
        } else {
          hourStr = str + "am";
        }
      }

      return month + " " + dayStr + " at " + hourStr;
    },
    async onSubmit(e) {
      e.preventDefault();
      if (!this.text || this.text.trim() === "") {
        alert("Please enter the task");
        return;
      }
      const newTask = {
        // id: Math.floor(Math.random() * 100000),
        text: this.text,
        day: await this.parseDate(this.day),
        reminder: this.reminder,
      };

      this.$emit("add-task", newTask);
      this.text = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>
<style scoped>
label {
  font-weight: 600;
  font-size: 20px;
}
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
input[type="submit" i] {
  width: 100%;
  padding: 10px 0;
  color: white;
  background: black;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px 0;
  box-sizing: border-box;
  padding: 3px 7px;
  font-size: 18px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>
