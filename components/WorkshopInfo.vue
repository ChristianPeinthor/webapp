<template>
  <div
    v-editable="blok"
    class="workshop-info"
  >
    <div class="left-content">
      <h2
        v-if="blok.subtitle"
        class="headline"
      >
        {{ blok.subtitle }}
      </h2>
    </div>
    <div class="right-content">
      <markdown
        v-if="blok.teaser"
        :value="blok.teaser"
        class="teaser"
      />
      <markdown
        v-if="blok.facts"
        :value="blok.facts"
        class="info-text"
      />
      <markdown
        v-if="blok.info"
        :value="blok.info"
        class="info-text"
      />
      <workshop-dates
        :dates="dates"
        :pretix="blok.pretix_shortform"
        class="workshop-dates"
     />
      <markdown
          v-if="blok.requirements"
          :value="blok.requirements"
          class="info-text"
      />
    </div>
    <div>
      <component v-for="i in blok.contentBloks" :blok="i" :is="i.component" :key="i.uid" />
    </div>
  </div>
</template>

<script>

import { getMetaTagsForPage } from '../services/MetaDataService'

export default {
  props: ['blok', 'dates'],
  data () {
    return {
    }
  },
  computed: {
    linktitle () {
      return this.blok.linktitle
    },
    images () {
      return {
        items: this.blok.images
      }
    }
  },
  head () {
    return getMetaTagsForPage(this.blok)
  }
}
</script>

<style lang="scss" scoped>

.workshop-info {
  color: #000;
  display: flex;
  flex-direction: column;
  flex: 1;
  justify-content: center;
  @include media-breakpoint-down(lg) {
    @include margin-page-wide;
  }
  .left-content {
    .headline {
      position: relative;
      @include media-breakpoint-up(md) {
        max-width: 50%;
        font-size: 2.2rem;
      }
      @include media-breakpoint-down(sm) {
        margin: 3vh 5%;
      }
      line-height: 1.5;
      font-family: $font-secondary;
    }
  }
  .right-content {
    flex-direction: column;
    position: relative;
    display: flex;
    align-items: flex-start;
    margin: 0 9%;
    @include media-breakpoint-down(lg) {
      margin: 0;
    }
    .workshop-dates {
      width: 100%;
      @include media-breakpoint-down(sm) {
        margin: 3vh 5%;
        width: 90%;
      }
    }
    .teaser, .info-text {
      font-weight: normal;
      font-family: $font-primary;
      line-height: 1.8;
      font-size: 1.1rem;
      @include media-breakpoint-down(sm) {
        line-height: 1.7;
        font-size: 1rem;
        margin: 0 0 0 5%
      }
    }
    .teaser {
      font-weight: bold;
    }
    .link {
      background-color: $color-orange;
      margin: 2% 0 0 5%;
      text-transform: uppercase;
      @include media-breakpoint-up(md) {
        margin-left: 25%;
      }
      color: #fff;
      padding: .7em .8em;
      font-weight: 800;
    }
  }
}
</style>
