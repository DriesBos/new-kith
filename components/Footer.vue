<template>
  <footer class="footer section-Footer" :class="{ active: showFooter }">
    <div class="footer-Background"></div>
    <div class="footer-Content">
      <ul>
        <li class="footer-Content_Title">
          <p>{{ general[0].content.footer_title }}</p>
        </li>
        <li>
          <markdown-item :input="general[0].content.footer_text" />
        </li>
        <nuxt-link to="/about" class="link cursorInteract">
          <span>Read our story</span>
          <div
            class="icon"
            v-html="require('~/assets/images/icon-arrow.svg?include')"
          />
        </nuxt-link>
        <form
          name="subscribe"
          method="post"
          action="/success"
          data-netlify="true"
          data-netlify-honeypot="bot-field"
          class="link cursorInteract"
        >
          <input type="hidden" name="form-name" value="contact" />
          <input
            type="text"
            required
            name="email"
            placeholder="Our newsletter..."
          />
          <button type="submit">
            <div
              class="icon"
              v-html="require('~/assets/images/icon-arrow.svg?include')"
            />
          </button>
        </form>
      </ul>

      <ul>
        <li class="hide"></li>
      </ul>
      <ul>
        <nuxt-link class="nav-Link link cursorInteract" to="/" tag="li"
          >Home</nuxt-link
        >
        <nuxt-link class="nav-Link link cursorInteract" to="/cases" tag="li"
          >Cases</nuxt-link
        >
        <nuxt-link class="nav-Link link cursorInteract" to="/talents" tag="li"
          >Talents</nuxt-link
        >
        <nuxt-link class="nav-Link link cursorInteract" to="/blog" tag="li"
          >What's happening</nuxt-link
        >
        <nuxt-link class="nav-Link link cursorInteract" to="/about" tag="li"
          >Our story</nuxt-link
        >
        <li class="desktop">&nbsp;</li>
        <nuxt-link
          class="desktop nav-Link link cursorInteract"
          to="/privacy-policy"
          tag="li"
          >Privacy Policy</nuxt-link
        >
        <li class="desktop">&nbsp;</li>
        <li class="desktop link link-Colophon cursorInteract">
          <a
            href="https://www.driesbos.com"
            target="_blank"
            rel="noreferrer"
            title="Site by Dries Bos"
          >
            Site by Dries Bos
          </a>
        </li>
      </ul>
      <ul>
        <li class="link cursorInteract">
          <div
            class="icon"
            v-html="require('~/assets/images/icon-mail.svg?include')"
          />
          <a
            :href="`mailto:${general[0].content.general_email}`"
            target="_blank"
            rel="noreferrer"
            title="mail"
          >
            {{ general[0].content.general_email }}
          </a>
        </li>
        <li class="link cursorInteract">
          <div
            class="icon"
            v-html="require('~/assets/images/icon-call.svg?include')"
          />
          <a
            :href="`tel:0031${general[0].content.general_phone_number}`"
            target="_blank"
            rel="noreferrer"
            title="call"
          >
            +31(0){{ general[0].content.general_phone_number }}
          </a>
        </li>
        <li class="link cursorInteract">
          <div
            class="icon"
            v-html="require('~/assets/images/icon-location.svg?include')"
          />
          <a
            :href="general[0].content.general_location"
            target="_blank"
            rel="noreferrer"
            title="directions"
          >
            Directions
          </a>
        </li>
        <li class="link cursorInteract">
          <div
            class="icon"
            v-html="require('~/assets/images/icon-instagram.svg?include')"
          />
          <a
            href="https://www.instagram.com/new.kith/"
            target="_blank"
            rel="noreferrer"
            title="instagram"
          >
            Instagram
          </a>
        </li>
        <li class="mobile">&nbsp;</li>
        <nuxt-link
          class="mobile nav-Link link cursorInteract"
          to="/privacy-policy"
          tag="li"
          >Privacy Policy</nuxt-link
        >
        <li class="mobile">&nbsp;</li>
        <li class="mobile link link-Colophon cursorInteract">
          <a
            href="https://www.driesbos.com"
            target="_blank"
            rel="noreferrer"
            title="Site by Dries Bos"
          >
            Site by Dries Bos
          </a>
        </li>
      </ul>
    </div>
    <nuxt-link class="footer-Logo cursorInteract" to="/" tag="div">
      <div v-html="require('~/assets/images/newkith-logo.svg?include')" />
    </nuxt-link>
    <script>
      ;(function(l, e, a, d, i, n, f, o) {
        if (!l[i]) {
          l.GlobalLeadinfoNamespace = l.GlobalLeadinfoNamespace || []
          l.GlobalLeadinfoNamespace.push(i)
          l[i] = function() {
            ;(l[i].q = l[i].q || []).push(arguments)
          }
          l[i].t = l[i].t || n
          l[i].q = l[i].q || []
          o = e.createElement(a)
          f = e.getElementsByTagName(a)[0]
          o.async = 1
          o.src = d
          f.parentNode.insertBefore(o, f)
        }
      })(
        window,
        document,
        "script",
        "https://cdn.leadinfo.net/ping.js",
        "leadinfo",
        "LI-6047499C276BE"
      )
    </script>
  </footer>
</template>

<script>
import { gsap } from "gsap"
import lodash from "lodash"
import { mapState } from "vuex"
import MarkdownItem from "@/components/MarkdownItem.vue"

export default {
  components: {
    "markdown-item": MarkdownItem
  },
  data() {
    return {
      scrollPosition: 0,
      showFooter: false
    }
  },
  computed: {
    ...mapState({
      general: state => state.general.list
    })
  },
  mounted() {
    this.handleDebouncedScroll = lodash.debounce(this.updateScrollPosition, 50)
    window.addEventListener("scroll", this.handleDebouncedScroll)
  },
  destroyed() {
    window.removeEventListener("scroll", this.handleDebouncedScroll)
  },
  methods: {
    updateScrollPosition() {
      this.scrollPosition = window.scrollY
      let scrollHeight = document.body.scrollHeight - window.innerHeight
      if (this.scrollPosition > scrollHeight - 20) {
        this.showFooter = true
      } else {
        this.showFooter = false
      }
      this.displayFooter()
    },
    displayFooter() {
      if (this.showFooter === true) {
        gsap.to(".footer-Background", {
          height: this.$el.offsetHeight,
          duration: "0.75",
          ease: "expo.out"
        })
        gsap.to(".header", {
          yPercent: "-100",
          duration: "0.75",
          ease: "expo.out"
        })
        gsap.to(".footer-Content", {
          opacity: "1",
          duration: "0.6",
          delay: "0.2",
          ease: "ease"
        })
        gsap.to(".footer-Logo", {
          opacity: "1",
          duration: "0.6",
          delay: "0.1",
          ease: "ease"
        })
        gsap.to(".footer", {
          backgroundColor: "#0202c4",
          duration: "0",
          delay: "0.75",
          ease: "ease"
        })
      } else {
        gsap.to(".footer-Background", {
          height: "0",
          duration: "0.65",
          delay: "0.25",
          ease: "expo.out"
        })
        gsap.to(".header", {
          yPercent: "0",
          duration: "0.65",
          delay: "0.25",
          ease: "expo.out"
        })
        gsap.to(".footer-Content", {
          opacity: "0",
          duration: "0.4",
          delay: "0.1",
          ease: "ease"
        })
        gsap.to(".footer-Logo", {
          opacity: "0",
          duration: "0.5",
          ease: "ease"
        })
        gsap.to(".footer", {
          backgroundColor: "black",
          duration: "0",
          delay: "0",
          ease: "ease"
        })
      }
    }
  }
}
</script>

<style lang="sass">
@import '~/assets/styles/variables.sass'

.footer
  color: white
  position: relative
  padding-top: var(--spacing-two)
  z-index: $z-footer
  display: flex
  flex-direction: column
  pointer-events: none
  max-height: 100vh
  overflow-y: auto
  .hide
    opacity: 0
  &.active
    pointer-events: auto
  &-Background
    position: absolute
    left: 0
    bottom: 0
    right: 0
    height: 0
    background: $support-color
    z-index: -1
  &-Content
    opacity: 0
    display: flex
    flex-wrap: wrap
    padding-left: var(--spacing-content-sides)
    padding-right: var(--spacing-content-sides)
    padding-bottom: var(--spacing-two)
    @media screen and (max-width: $breakpoint-laptop)
      justify-content: flex-end
    &_Title
      margin-bottom: 1.55rem
    ul
      flex-basis: 25%
      padding-right: var(--spacing-two)
      &:last-child
        padding-right: 0
    @media screen and (max-width: $breakpoint-laptop)
      ul
        flex-basis: 50%
      ul:nth-child(2)
        display: none
    @media screen and (max-width: $breakpoint-mobile)
      ul
        flex-basis: 100%
        margin-bottom: var(--spacing-two)
    li
      .icon
        margin-right: .5rem
    a
      text-decoration: none
  &-Logo
    opacity: 0
    padding-left: var(--spacing-content-sides)
    padding-right: var(--spacing-content-sides)
    padding-bottom: var(--spacing-two)
    svg
     fill: white !important
</style>
