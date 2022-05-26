<template>
  <body>
    <v-btn :disabled="!isBtnValid" @click="createTable()" style="width: 150px"
      >Сгенерировать</v-btn
    >
  </body>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    isBtnValid: true,
  }),
  methods: {
    makeString(length) {
      let result = "";
      let characters = "абвгдеёжзийклмнопрстуфхцчшщъыьэюя";
      let charactersLength = characters.length;
      for (let i = 0; i < length; i++) {
        result += characters.charAt(
          Math.floor(Math.random() * charactersLength)
        );
      }
      return result;
    },
    createTable() {
      this.isBtnValid = false;
      let tbl = document.createElement("table");
      let tblBody = document.createElement("tbody");
      let price;
      let count;
      let sum = 0;
      for (let i = 0; i < 50; i++) {
        let row = document.createElement("tr");

        for (let j = 0; j < 4; j++) {
          let cell = document.createElement("td");
          if (j === 0) {
            var cellText = document.createTextNode(this.makeString(5));
          } else if (j === 1) {
            cellText = document.createTextNode(
              (price = Math.floor(Math.random() * 1000.0) + 0.01)
            );
          } else if (j === 2) {
            cellText = document.createTextNode(
              (count = Math.floor(Math.random() * 100) + 1)
            );
          } else if (j === 3) {
            let number = (parseFloat(price) * parseInt(count)).toFixed(2);
            sum += parseFloat(number);
            cellText = document.createTextNode(number);
          }
          cell.appendChild(cellText);
          row.appendChild(cell);
        }

        tblBody.appendChild(row);
      }

      tbl.appendChild(tblBody);
      document.body.appendChild(tbl);
      tbl.setAttribute("border", "2");

      tbl.after("Итоговая стоимость:" + sum.toFixed(3).toString());
    },
  },
};
</script>
