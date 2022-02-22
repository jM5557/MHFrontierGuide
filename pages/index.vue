<template>
  <div>
    <div class = "notice">
      <div class="inner">
        <b>PLEASE READ</b>
        <b :style = "{ color: 'red', fontSize: '1.25rem' }">[ This guide is under construction ]</b>
        <p>
          Monster Hunter Frontier was an MMO that ran from 2007 - 2019. Servers were shut down in 2019, rendering over a decade's worth of content inaccesible to the general public.
          <br />
          However, through the hard work, dedication, efforts, and numerous hours spent by the ErupeServer team, it is now possible to run a private server, allowing you to launch and play the game to a limited capacity.
          There are many in-game features, many still unknown, that may break or are simply inaccessible. However, the setup included in this guide contains necessary files for progressing into G-Rank.
          <br />
          The guide and downloadable files provided in this site are a compilation of everything needed to setup and run Monster Hunter Frontier playable on a Windows 10 computer.
          This guide is built upon Ricochhet's ErupeServer documentation <a href="https://github.com/ricochhet/Erupe" class = "source-link">available on GitHub</a> Please refer to this for additional/detailed information.
          <br />
          We do NOT claim ownership or involvement in the creation of the ErupeServer source code. We do NOT take credit for any of the work done to bring this game back to life.
          <br />
          Our intention is to simplify the setup process in order for new players to try the game.
          <br />
          We do NOT condone the monetization or profiteering of any of the files, data, or materials provided in this site. Everyone should be able to enjoy this great game.
          <br />
          Please be respectful, have fun, and...
          <br />
          <b>Happy Hunting!</b>
        </p>
        <a class = "next" href = "#hero-downloads">
          Next
        </a>
      </div>
    </div>
    <div class="hero" id = "hero-downloads">
        <div 
          class="menu-btn" 
          id = "menu-btn" 
          v-on:click="() => this.menuIsOpen = !this.menuIsOpen"
        >
          <img alt = "menu button" src = "assets/images/menu-icon.svg" />
          <span>Menu</span>
        </div>
        <ul v-if="menuIsOpen" id = "menu">
            <li>
                <a href="#requirements">
                    Requirements
                </a>
            </li>
            <li
              v-for="(mdContentItem, index) in mdContent"
              v-bind:key = "index"
            >
              <a v-bind:href = "`#${ mdContentItem.attributes.slug }`">
                {{ mdContentItem.attributes.title }}
              </a>
            </li>
        </ul>
        <div class="logo">
            <img src="assets/images/mhfz-logo.png" alt="Monster Hunter Frontier Z logo">
        </div>
        <a href="https://drive.google.com/drive/folders/1YbsKRs8AUESblojsRITZcRqaObvnOoFS?usp=sharing" class="cta">
          <DownloadIcon />
          <span>Downloads</span>
        </a>
    </div>
    <div class="section requirements" id = "requirements">
        <div class="inner">
            <div class="left">
                <h1>Requirements</h1>
                <h2>Before getting started, download the following required items:</h2>
            </div>
            <div class="right">
                <ul class = "checkbox-items">
                    <CheckboxItem
                      v-for="requirement in requirements"
                      v-bind:key="requirement"
                      :text="requirement"
                    />
                </ul>
                <br />
                <p>The Google Drive download page should look like below:</p>
                <br />
                <ClickableImage alt = "downloads" src = "assets/images/downloads.jpg" />
            </div>
        </div>
    </div>
    <div
      v-for="(mdContentItem, index) in mdContent"
      v-bind:key = "index"
      :class = "`section ${ mdContentItem.attributes.title }`"
      :id = "mdContentItem.attributes.slug"
    >
      <Section :markdownContent="mdContentItem" />
    </div>

    <div class="disclaimer">
        <p>This is a fan-site. All content is trademarked and owned by CAPCOM Co., Ltd</p>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Section from '~/components/Section.vue';
import CheckboxItem from '~/components/CheckboxItem.vue';
import ClickableImage from '~/components/ClickableImage.vue';
import DownloadIcon from "~/assets/images/download-icon.svg?inline";

var amount: number = 0;

const fm = require("front-matter");
var md = require("markdown-it")({
  html: true,
  typographer: true
}).enable('image');

export default Vue.extend({
  name: 'IndexPage',
  data () {
    return {
      menuIsOpen: false,
      requirements: [
        'MHFrontierSetup.zip',
        'PostgreSQL',
        'Python 3.8 Installer',
        'Go Installer (CLI)'
      ]
    }
  },
  async asyncData() {
    const mdFiles = [
      await import(`~/markdown/setup.md`),
      await import(`~/markdown/troubleshooting.md`)
    ];

    const mdContent = [];

    for (let i = 0; i < mdFiles.length; i++) {
      let res = fm(mdFiles[i].default);
      mdContent.push({
        attributes: res.attributes,
        content: md.render(res.body)
      });
    }

    return {
      mdContent
    }
  },
  mounted: function () {
      let codes: HTMLCollectionOf<HTMLElement> = document.getElementsByTagName("code");
      for (let i: number = 0; i < codes.length; i++) {
        let str: string = codes[i].innerText;
        let btn: HTMLButtonElement = document.createElement("button");
        
        btn.className = "code-copy";
        btn.innerText = "Copy";
        
        btn.addEventListener("click", function (e:any) {
          e.preventDefault();
          navigator.clipboard.writeText(str);
          if (amount < 3) {
            let div = document.createElement("div");
            div.className = "banner";
            div.innerText = "Copied Text to Clipboard!";
            
            document.body.appendChild(div);
            setTimeout(
              () => { div.remove(); amount--; },
              4000
            )

            amount++;
          }
        });
        
        codes[i].appendChild(btn);
      }
  },
  components: {
    Section,
    CheckboxItem,
    ClickableImage,
    DownloadIcon
  }
})
</script>

<style lang="scss" scoped>
  @import "/assets/scss/main.scss";
</style>
