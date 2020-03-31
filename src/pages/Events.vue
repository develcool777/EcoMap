<template>
  <div class="fixed">
    <Header :style="{ background: dark }"/>
    <EventContent :dataItems="items"/>
    <Footer/>
  </div>
</template>

<script>
import Header from '@/layout/header'
import EventContent from '@/layout/events'
import Footer from '@/layout/footer'
export default {
  name: 'Event',
  components: {
    Header,
    EventContent,
    Footer
  },
  data () {
    return {
      dark: '#1B1919',
      items: [
        { id: 0, url: 'img1.png', title: 'Majorka beach', trash: 'Trash', place: 'Beach', date: '25.01.2020', text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt.', btn: 'Read more', rating: 4.1 },
        { id: 1, url: 'img1.png', title: 'Majorka beach', trash: 'Trash', place: 'Beach', date: '25.01.2020', text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt.', btn: 'Read more', rating: 4.1 },
        { id: 2, url: 'img1.png', title: 'Majorka beach', trash: 'Trash', place: 'Beach', date: '25.01.2020', text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt.', btn: 'Read more', rating: 4.1 },
        { id: 3, url: 'img1.png', title: 'Majorka beach', trash: 'Trash', place: 'Beach', date: '25.01.2020', text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt.', btn: 'Read more', rating: 4.1 },
        { id: 4, url: 'img1.png', title: 'Majorka beach', trash: 'Trash', place: 'Beach', date: '25.01.2020', text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt.', btn: 'Read more', rating: 4.1 },
        { id: 5, url: 'img1.png', title: 'Majorka beach', trash: 'Trash', place: 'Beach', date: '25.01.2020', text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt.', btn: 'Read more', rating: 4.1 },
        { id: 6, url: 'img1.png', title: 'Majorka beach', trash: 'Trash', place: 'Beach', date: '25.01.2020', text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt.', btn: 'Read more', rating: 4.1 },
        { id: 7, url: 'img1.png', title: 'Majorka beach', trash: 'Trash', place: 'Beach', date: '25.01.2020', text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt.', btn: 'Read more', rating: 4.1 },
        { id: 8, url: 'img1.png', title: 'Majorka beach', trash: 'Trash', place: 'Beach', date: '25.01.2020', text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt.', btn: 'Read more', rating: 4.1 },
        { id: 9, url: 'img1.png', title: 'Majorka beach', trash: 'Trash', place: 'Beach', date: '25.01.2020', text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt.', btn: 'Read more', rating: 4.1 }
      ]
    }
  }
}
</script>
<style lang="scss">
</style>
