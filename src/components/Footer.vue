<template>
    <footer id="footer">
        <div id="footer-left" class="footer-box">
            <h2 id="signed">{{ leftString }}</h2>
        </div>
        <div id="footer-center" class="footer-box">
            <h1>{{ centerString.head }}</h1>
            <p>{{ centerString.body }}</p>
        </div>
        <div id="footer-right" class="footer-box">
            <h2 id="copyright">{{ rightString }}</h2>
        </div>
    </footer>
</template>

<script>
import { Vue } from 'vue-property-decorator'

const Footer = Vue.extend({
  data () {
    return {
      leftString: 'admin@durbantech.com',
      centerString: {
        head: 'Design by DurbanTech',
        body: 'Oklahoma City, Oklahoma, USA'
      },
      rightString: 'Copyright 2021'
    }
  }
})
export default Footer
</script>

<style scoped>
#footer {
    width: 100%;
    position: fixed;
    bottom: 0;
    margin: 0;
    background: var(--footer-bg-light);
    color: var(--font-dark);
    border-top: 2px solid var(--border-light-soft);
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-between;
    align-content: flex-end;
    align-items: center;
    overflow: hidden;
}
.footer-box {
    /* height: 90%; */
    width:auto;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
    align-items: center;
    margin-top: 0;
    padding: 5px;
    margin: 0.1rem;
    overflow: hidden;
}
#footer-center {
    align-items: center;
    width: 50%;
    border-left: 1px solid black;
    border-right: 1px solid black;
}
h1 {
    margin: 0 1rem;
    font-size: 11pt;
}
h2 {
    margin: 0 1rem;
    font-size: 10pt;
}
p {
    font-size: 9pt;
    margin: 0.3rem;
}

@media screen and (max-width:600px) {
  #footer-center>p {
    display:none;
  }
  h1 {
      margin: 0;
      font-size: 10pt;
  }
  h2 {
      margin: 0;
      font-size:8pt;
  }
  h3 {
      font-size: 8pt;
  }
}
</style>
