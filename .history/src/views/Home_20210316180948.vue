<template>
    <div class="container">
        <div class="row">
            <div class="title-text">
                <p>CSV Import</p>
            </div>
        </div>
        <div class="row file-btn">
            <label class="custom-file-upload">
                <input type="file" id="csv" name="csv_file" class="button-control" @change="loadCSV($event)">
                Choose File
            </label>
        </div>
        <table v-if="parse_csv">
            <thead>
                <tr>
                    <th v-for="key in parse_header" 
                        @click="sortBy(key)" 
                        :class="{ active: sortKey == key }"
                        :key="key"
                    >
                        {{ key | capitalize }}
                        <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'"></span>
                    </th>
                </tr>
            </thead>
            <tr v-for="csv in parse_csv" :key="csv">
                <td v-for="key in parse_header" :key="key">
                    {{ csv[key] }}
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
    name: 'Home',
    data() {
        return {
            channel_name: '',
            channel_fields: [],
            channel_entries: [],
            parse_header: [],
            parse_csv: [],
            sortOrders:{},
            sortKey: '',
            result: []
        }
    },
    filters: {
      capitalize: function (str) {
        return str.charAt(0).toUpperCase() + str.slice(1)
      }
    },
    methods: {
      sortBy(key) {
        var vm = this
        vm.sortKey = key
        vm.sortOrders[key] = vm.sortOrders[key] * -1
      },
      csvJSON(csv){
        var vm = this
        var lines = csv.split("\n")
        var result = []
        var headers = lines[0].split(",")
        vm.parse_header = lines[0].split(",") 
        lines[0].split(",").forEach(function (key) {
          vm.sortOrders[key] = 1
        })
        
        lines.map(function(line, indexLine){
          if (indexLine < 1) return // Jump header line
          
          var obj = {}
          var currentline = line.split(",")
          
          headers.map(function(header, indexHeader){
            obj[header] = currentline[indexHeader]
          })
          
          result.push(obj)
        })
        
        result.pop() // remove the last item because undefined values
        
        return result // JavaScript object
      },
      loadCSV(e) {
        var vm = this
        if (window.FileReader) {
          var reader = new FileReader();
          reader.readAsText(e.target.files[0]);
          // Handle errors load
          reader.onload = function(event) {
            var csv = event.target.result;
            vm.parse_csv = vm.csvJSON(csv)
            
          };
          reader.onerror = function(evt) {
            if(evt.target.error.name == "NotReadableError") {
              alert("Canno't read file !");
            }
          };
        } else {
          alert('FileReader are not supported in this browser.');
        }
      },

    }
}
</script>

<style scoped>

</style>