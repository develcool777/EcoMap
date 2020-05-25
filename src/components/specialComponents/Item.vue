<template>
  <div class="Item">
    <img :src=" require('../../assets/Items/' + fitem.issue.url )" alt="image" class="Item__img">
    <div class="Item__info">
      <div class="Item__title">{{ fitem.issue.title }}</div>
      <div class="Item__datePlace">
        <div class="Item__trash">{{ fitem.issue.pollution_category }}</div>
        <div class="Item__date">{{ fitem.issue.date }}</div>
      </div>
      <div class="Item__pollution">Polution rating: {{ fitem.issue.pollution_rating }}</div>
      <div class="Item__text">{{ fitem.issue.description }}</div>
      <button class="Item__btn">Read more</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Item',
  props: {
    fitem: {
      type: Object
    }
  }
}
</script>
<style lang="scss">
.Item {
  display: flex;
  justify-content: space-between;
  margin: 0 0 rem(40);
  width: rem(560);
  color: $gray;
  &__info {
    width: rem(350);
  }
  &__title {
    font-style: normal;
    font-weight: 500;
    font-size: rem(26);
  }
  &__datePlace {
    @include FCenter(space-between);
    width: rem(265);
  }
  &__datePlace, &__pollution, &__text, &__btn {
    font-size: rem(20);
    line-height: 24px;
  }
  &__datePlace, &__text {
    padding: rem(5) 0;
  }
  &__text {
    max-height: rem(70);
    overflow: hidden;
  }
  &__btn {
    border: none;
    outline: none;
    background: none;
    padding: 0;
    color: $gray;
    position: relative;
    transition-duration: .5s;
    font-size: rem(24);
  }
  &__btn:after {
    content: "";
    position: absolute;
    top: 8px;
    right: -15px;
    border: solid $gray;
    border-width: 0 2px 2px 0;
    display: block;
    padding: 5px;
    transform: rotate(-45deg);
    transition-duration: .5s;
  }
  &__btn:hover {
    color: $white;
    cursor: pointer;
  }
  &__btn:hover:after {
    border-color: $red;
    cursor: pointer;
  }
}
</style>
