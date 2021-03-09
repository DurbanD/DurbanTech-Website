<template>
  <div class="about">
    <div id="about-head">
      <h1>{{ headTextLarge }}</h1>
      <p>{{ headTextSmall }} </p>
    </div>
    <h2 id="service-head">Services</h2>
    <div id="about-boxes">

      <AboutBox
      id="about-box-left"
      :head="content.left.head"
      :listItems="content.left.listItems" />

      <AboutBox
      id="about-box-left"
      :head="content.right.head"
      :listItems="content.right.listItems" />
    </div>
  </div>
</template>

<script>
import { Vue } from 'vue-property-decorator'
import AboutBox from '../components/AboutBox'

const About = Vue.extend({
  data () {
    return {
      headTextLarge: 'About Durban Technology',
      headTextSmall: 'DurbanTech offers a wide range of services to clients both near and far. Below you will see an overview of said services. Click each item or visit our contact page for more information.',
      content: {
        left: {
          head: 'Local',
          listItems: [
            {
              main: 'Network & Server Administration',
              expanded: 'Custom internal networks and servers are invaluable to any sizeable businesses, and for good reason. The usefulness of having your home or office interconnected cannot be understated, and in many ways the sky is the limit. From a home media server to an office of hundreds of interconnected devices - make sure your digital home is fast, secure, and useful.'
            },
            {
              main: 'Computer & Android Repair',
              expanded: 'Broken screen? Temperamental Keyboard? Not sure what could be wrong with your device? We offer all manner of troubleshooting and repairs for laptops, personal computers, and Android phones.'
            },
            {
              main: 'Small Business Solutions',
              expanded: 'For entrepenuers who need a little more. DurbanTech can help you assess exactly what you need to ensure you get the absolute most out of your technology.'
            },
            {
              main: 'National Services',
              expanded: 'Anything offered to our National (US) clients are proudly served to our local clients as well.'
            }
          ]
        },
        center: {
          head: '',
          listItems: []
        },
        right: {
          head: 'National',
          listItems: [
            {
              main: 'Website Design & Management',
              expanded: 'Whether you are an individual, a brick-and-mortar shop, or an e-commerce etrepenuer, a responsive, modern website is essential. We can build what you need, how you need it - fast. '
            },
            {
              main: 'Software Development',
              expanded: 'Do you need software to do something very specific? We will work with you to develop exactly the software you need, built from the best technologies available for the task at hand.'
            },
            {
              main: 'Network Administration',
              expanded: 'With the help of modern technology, many networks can be monitored and administered to remotely from all over the world. A powerful solution that can even allow your business to manage multiple independent networks at once!'
            },
            {
              main: 'Consultation',
              expanded: 'If you are uncertain about what exactly you may need, or have an idea without the know-how, we can offer our expertise to get you to the best solution. Use our convenient contact form for more information.'
            }
          ]
        }
      }
    }
  },
  components: {
    AboutBox
  }
})
export default About
</script>

<style scoped>
.about {
  display: flex;
  flex-flow: column;
  align-items: center;
}
#about-head {
  margin: 1rem 1rem 0.5rem 1rem;
  padding: 0;
  width: 100%;
}
#about-boxes {
  margin: 0 1rem;
  width: 100%;
  display: flex;
  flex-flow: row;
  justify-content: space-evenly;
  align-items: flex-start;
  align-content: center;
  line-height: 1.7rem;
  overflow: hidden;
}
h1 {
  margin: 0;
  padding: 0;
  justify-self: flex-start;
}
h2 {
  margin: 0;
  padding: 0;
}
p {
  margin: 0;
  margin-bottom: 0;
  padding: 1rem 1rem 0.5rem 1rem;
  border-bottom: 1px dotted var(--primary-light-transparent);
}
#service-head {
  margin: 0;
  padding-top: 0;
  padding-bottom: 5px;
  width: 30%;
  border-bottom: 1px dotted var(--primary-light-transparent);
  border-right: 1px dotted var(--primary-light-transparent);
  border-left: 1px dotted var(--primary-light-transparent);
}
</style>
