<template>
  <section class="section section-Logos section-TextContent carouselOnScroll">
    <p>Our partners:</p>
    <div class="section-Logos_Content">
      <div class="carouselOnScroll-Wrapper">
        <ul>
          <component
            :is="blok.component | dashify"
            v-for="blok in blok.body"
            :key="blok._uid"
            :blok="blok"
          ></component>
          <component
            :is="blok.component | dashify"
            v-for="blok in blok.body"
            :key="blok._uid + '1'"
            :blok="blok"
          ></component>
          <component
            :is="blok.component | dashify"
            v-for="blok in blok.body"
            :key="blok._uid + '2'"
            :blok="blok"
          ></component>
          <component
            :is="blok.component | dashify"
            v-for="blok in blok.body"
            :key="blok._uid + '3'"
            :blok="blok"
          ></component>
          <component
            :is="blok.component | dashify"
            v-for="blok in blok.body"
            :key="blok._uid + '4'"
            :blok="blok"
          ></component>
          <component
            :is="blok.component | dashify"
            v-for="blok in blok.body"
            :key="blok._uid + '5'"
            :blok="blok"
          ></component>
          <component
            :is="blok.component | dashify"
            v-for="blok in blok.body"
            :key="blok._uid + '6'"
            :blok="blok"
          ></component>
          <component
            :is="blok.component | dashify"
            v-for="blok in blok.body"
            :key="blok._uid + '7'"
            :blok="blok"
          ></component>
          <component
            :is="blok.component | dashify"
            v-for="blok in blok.body"
            :key="blok._uid + '8'"
            :blok="blok"
          ></component>
          <component
            :is="blok.component | dashify"
            v-for="blok in blok.body"
            :key="blok._uid + '9'"
            :blok="blok"
          ></component>
        </ul>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    blok: Object
  }
}
</script>

<style lang="sass">
@import '~/assets/styles/variables.sass'

.section-Logos
    padding-left: 0
    padding-right: 0
    p
        margin-left: var(--spacing-content-sides)
        margin-bottom: var(--spacing-one)
    &_Content
        width: 100vw
        overflow-x: auto
        display: flex
        flex-wrap: nowrap
        border-top: $border
        border-bottom: $border
        padding-top: 2rem
        padding-bottom: 2rem
    ul
        display: flex
        flex-wrap: nowrap
        height: 5.5rem
</style>
