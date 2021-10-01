<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

//grid ---------------------
.row {
  margin-left: -8px;
  margin-right: -8px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

$col-step: 12;

.col-1,
.col-2,
.col-3,
.col-4,
.col-5,
.col-6,
.col-7,
.col-8,
.col-9,
.col-10,
.col-11,
.col-12 {
  padding-left: 8px;
  padding-right: 8px;
}

@for $i from 1 through $col-step {
  $calc: #{100% / 12 * $i};

  .col-#{$i} {
    flex: 0 0 $calc;
    max-width: $calc;
  }
}

// space -------------------
$step: 25;
$interval: 4;

@for $i from 0 through $step {
  .m-t-#{$i*$interval} {
    margin-top: #{$i * $interval}px !important;
  }
}

@for $i from 0 through $step {
  .m-r-#{$i*$interval} {
    margin-right: #{$i * $interval}px !important;
  }
}

@for $i from 0 through $step {
  .m-b-#{$i*$interval} {
    margin-bottom: #{$i * $interval}px !important;
  }
}

@for $i from 0 through $step {
  .m-l-#{$i*$interval} {
    margin-left: #{$i * $interval}px !important;
  }
}

@for $i from 0 through $step {
  .p-t-#{$i*$interval} {
    padding-top: #{$i * $interval}px !important;
  }
}

@for $i from 0 through $step {
  .p-r-#{$i*$interval} {
    padding-right: #{$i * $interval}px !important;
  }
}

@for $i from 0 through $step {
  .p-b-#{$i*$interval} {
    padding-bottom: #{$i * $interval}px !important;
  }
}

@for $i from 0 through $step {
  .p-l-#{$i*$interval} {
    padding-left: #{$i * $interval}px !important;
  }
}
</style>
