<script setup>
import plain_data from '~/assets/data.yaml'
import { onMounted, nextTick, reactive } from 'vue'

const data = reactive(plain_data)

useHead({
  title: data.name,
  link: [
    { rel: 'stylesheet', href: 'https://use.typekit.net/vxy8tas.css' },
    { rel: 'stylesheet', href: 'https://use.typekit.net/jge8wgr.css' },
  ],
  meta: [
    {
      name: 'description',
      content: `The homepage of ${data.name}`,
    },
    // {
    //   name: "google-site-verification",
    //   content: "",
    // },
  ],
})

useSeoMeta({
  title: data.name,
  ogTitle: data.name,
  description: `The homepage of ${data.name}`,
  ogDescription: `The homepage of ${data.name}`,
  ogImage: 'https://allen-peng-yl.github.io/images/profile.jpg',
  twitterCard: 'summary_large_image',
})


onMounted(() => {
})
</script>

<template>
  <div id="app">
    <img src="/images/profile.jpg" alt="profile pic" id="profile-pic">
    <div id="profile">
      <div class="myname">{{ data.name }}</div>
      <div class="mytitle" v-if="data.title">{{ data.title }}</div>
      <div v-for="profile in data.profiles"><span v-html="profile"></span></div>
    </div>
    <p v-for="bio in data.bios"><span v-html="bio"></span></p>

    <hr>

    <div id="projects">
      <h2>Working Experience</h2>
      <div class="project" v-for="project in data.projects">
        <h3>
          <div>{{ project.title }}</div>
          <div class="subtitle">
            <div>{{ project.role }}</div>
            <div>{{ project.date }}</div>
          </div>
        </h3>
        <div class="logo"><img v-if="project.thumbnail" :src="project.thumbnail" :alt="project.title + ' logo'" loading="lazy"></div>
        <div class="contents">
          <ul>
            <li v-for="description in project.descriptions">
              <template v-if="description.text">
                <span v-html="description.text"></span>
                <ul>
                  <li v-for="sub in description.sub" v-html="sub"></li>
                </ul>
              </template>
              <span v-else v-html="description"></span>
            </li>
          </ul>
          <div class="link" v-for="[linkName, link] in Object.entries(project.links)">
            [<a :href="link" target="_blank">{{ linkName }}</a>]
          </div>
        </div>
        <hr>
      </div>
    </div>

    <div id="education">
      <h2>Education</h2>
      <div class="project" v-for="edu in data.education">
        <h3>
          <div>{{ edu.degree }}</div>
          <div class="subtitle">
            <div>{{ edu.institution }}</div>
            <div>{{ edu.date }}</div>
          </div>
        </h3>
        <div class="logo"><img v-if="edu.thumbnail" :src="edu.thumbnail" :alt="edu.institution + ' logo'" loading="lazy"></div>
        <div class="contents">
          <ul>
            <li v-for="description in edu.descriptions" v-html="description"> </li>
          </ul>
        </div>
        <hr>
      </div>
    </div>

    <div id="leadership">
      <h2>Leadership &amp; Service</h2>
      <div class="project" v-for="item in data.leadership">
        <h3>
          <div>{{ item.title }}</div>
          <div class="subtitle">
            <div>{{ item.role }}</div>
            <div>{{ item.date }}</div>
          </div>
        </h3>
        <hr>
      </div>
    </div>

    <div id="pubs">
      <h2>Selected Publications</h2>
      <div class="entry" v-for="pub in data.publications">
        <div class="entry-title">{{ pub.title }}</div>
        <div v-html="pub.authors"></div>
        <div>
          <span class="venue">{{ pub.venue }}</span>
          <span class="link" v-for="[linkName, link] in Object.entries(pub.links)">
            [<a :href="link" target="_blank">{{ linkName }}</a>]
          </span>
        </div>
      </div>
    </div>

    <div id="presentations">
      <h2>Conference Presentations</h2>
      <div class="entry" v-for="pres in data.presentations">
        <div class="entry-title">{{ pres.title }}</div>
        <div><span class="venue">{{ pres.venue }}</span> ({{ pres.type }})</div>
      </div>
    </div>

  </div>
</template>

<style>
body {
  /*font-family: -apple-system,system-ui,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;*/
  font-family: "proxima-nova", sans-serif;
  color: #303030;
  background-color: #f6f6f5;
}

h2 {
  font-family: "factoria", sans-serif;
  font-weight: 700;
  font-size: 20pt;
}

a {
  color: #303030;
  text-decoration: none;
  position: relative;
  white-space: nowrap;
  cursor: pointer;
  transition: all 500ms cubic-bezier(0, 0.8, 0.13, 1);
}

a:after {
  content: '';
  position: absolute;
  z-index: -1;
  top: 66%;
  left: -0.1em;
  right: -0.1em;
  bottom: 0;
  transition: all 500ms cubic-bezier(0, 0.8, 0.13, 1);
  background-color: #F3CFC6bb;
}

@media (hover: hover) {
  a:hover {
    color: #fff;
  }

  a:hover:after {
    top: 0%;
    background-color: #9F2B68;
  }
}

a:hover {
  color: #fff;
}

a:active:after {
  top: 0%;
  background-color: #002D72;
}

hr {
  border: solid #D5D0C0 1px;
}

div#app {
  margin: 0 10%;
  padding-bottom: 50px;
}

.myname {
  margin: 30px 0 8px 0;
  font-family: "factoria", sans-serif;
  font-weight: 700;
  font-size: 30pt;
}

.mytitle {
  margin-bottom: 25px;
  font-size: 13pt;
  color: #002D72;
}

div#profile {
  vertical-align: top;
  padding: 0 20px;
  display: inline-block;
  max-width: calc(100% - 230px);
}

@media (max-width: 800px) {
  div#profile {
    padding: initial;
    max-width: initial;
  }
}

img#profile-pic {
  padding: 15px 0;
  width: 150px;
}

/*
@media (max-width: 800px) {
img#profile-pic {
  display: none;
}
}
*/

div#projects h3 .subtitle,
div#education h3 .subtitle,
div#leadership h3 .subtitle {
  display: flex;
  justify-content: space-between;
  font-weight: normal;
  font-size: 12pt;
}

div#projects div.link,
div#pubs div.link {
  display: inline;
  margin-right: 5px;
}

div#projects .logo,
div#education .logo {
  display: inline-block;
  vertical-align: top;
  width: 80px;
}

div#projects .logo img,
div#education .logo img {
  width: 80px;
  max-height: 80px;
  object-fit: contain;
  mix-blend-mode: multiply;
}

div#projects .contents,
div#education .contents {
  vertical-align: top;
  margin-left: 20px;
  display: inline-block;
  max-width: calc(100% - 120px);
}

div#projects .contents ul,
div#education .contents ul {
  margin-top: 0;
}

.entry {
  padding: 12px 0;
  border-bottom: 2px solid #D5D0C0;
  line-height: 1.5;
}

.entry .entry-title {
  font-weight: 700;
  font-size: 13pt;
}

.entry .venue {
  font-style: italic;
  margin-right: 6px;
}

@media (max-width: 800px) {

  div#projects .logo,
  div#education .logo {
    display: none;
  }

  div#projects .contents,
  div#education .contents {
    vertical-align: initial;
    margin-left: initial;
    display: initial;
    max-width: initial;
  }
}

.hide {
  opacity: 0;
  transition: opacity .3s;
}

.hide:hover {
  opacity: 1;
}
</style>
