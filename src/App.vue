<template>
  <div id="app">
    <p>(You can double click on an item to turn it into a folder.)</p>
    <ul>
      <TreeItem
        class="item"
        :item="treeData"
        @make-folder="makeFolder"
        @add-item="addItem"
      >
      </TreeItem>
    </ul>
  </div>
</template>

<script>
import TreeItem from './components/TreeItem.vue'
import Vue from 'vue'

var treeData = {
  name: "My Tree",
  children: [
    { name: "hello" },
    { name: "wat" },
    {
      name: "child folder",
      children: [
        {
          name: "child folder",
          children: [{ name: "hello" }, { name: "wat" }]
        },
        { name: "hello" },
        { name: "wat" },
        {
          name: "child folder",
          children: [{ name: "hello" }, { name: "wat" }]
        }
      ]
    }
  ]
};

export default {
  name: 'App',
  components: {
    TreeItem
  },
  data() {
    return {
      treeData: treeData
    }
  },
  methods: {
    makeFolder: function(item) {
      Vue.set(item, "children", []);
      this.addItem(item);
    },
    addItem: function(item) {
      item.children.push({
        name: "new stuff"
      })
    }
  }
}
</script>

<style>
body {
  font-family: Menlo, Consolas, monospace;
  color: #444;
}
.item {
  cursor: pointer;
}
.bold {
  font-weight: bold;
}
ul {
  padding-left: 1em;
  line-height: 1.5em;
  list-style-type: dot;
}
</style>
