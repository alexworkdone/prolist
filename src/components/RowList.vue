<template>
  <div class="row">
    <div class="col-1">{{ num }}</div>
    <div class="col-8" :class="{ mark: newRow }">
      {{ row.name }}
    </div>
    <div class="col-3" :class="{ mark: colCount }">
      {{ row.count }}
    </div>
  </div>
</template>

<script>
export default {
  name: "RowList",

  props: {
    row: Object,
    num: [Number, String],
    newRow: Boolean,
    colCount: Boolean,
  },
};
</script>

<style lang="scss">
[class^="col-"] {
  position: relative;
  padding: 4px 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid #333;

  &.mark:after {
    content: "";
    position: absolute;
    top: 4px;
    right: 4px;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background-color: red;
  }
}

.col-8 {
  justify-content: flex-start;
}

.table-header {
  padding-bottom: 16px;
  font-size: 1.2em;
  font-weight: 700;

  [class^="col-"] {
    padding-top: 16px;
    padding-bottom: 16px;
  }
}

textarea {
  padding: 4px 8px;
  width: 100%;
  border: none;
}
</style>
