<script setup>
import FormSearch from '@/components/FormSearch.vue'
</script>

<template>
  <div>
    <FormSearch />
  </div>
</template>

<style lang="scss">
@import url('https://fonts.cdnfonts.com/css/campton');

* {
  font-family: 'Campton', sans-serif;
}

html {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  height: 100svh;
  width: 100vw;
}

.d-flex {
  display: flex;
}

.flex-column {
  flex-direction: column;
}

.flex-row {
  flex-direction: row;
}

.align-center {
  align-items: center;
}

.align-end {
  align-items: flex-end;
}

.justify-center {
  justify-content: center;
}

.justify-space-between {
  justify-content: space-between;
}

.justify-end {
  justify-content: flex-end;
}

.gap {
  @for $i from 1 through 16 {
    &-#{$i} {
      gap: 4px * $i;
    }
  }
}

.pa {
  @for $i from 0 through 16 {
    &-#{$i} {
      padding: 4px * $i;
    }
  }
}

.py {
  @for $i from 0 through 16 {
    &-#{$i} {
      padding-top: 4px * $i;
      padding-bottom: 4px * $i;
    }
  }
}

.px {
  @for $i from 0 through 16 {
    &-#{$i} {
      padding-left: 4px * $i;
      padding-right: 4px * $i;
    }
  }
}

.ma {
  @for $i from 0 through 16 {
    &-#{$i} {
      margin: 4px * $i;
    }
  }
}

.my {
  @for $i from 0 through 16 {
    &-#{$i} {
      margin-top: 4px * $i;
      margin-bottom: 4px * $i;
    }
  }
}

.mx {
  @for $i from 0 through 16 {
    &-#{$i} {
      margin-left: 4px * $i;
      margin-right: 4px * $i;
    }
  }
}

.cursor-pointer {
  cursor: pointer;
}
</style>