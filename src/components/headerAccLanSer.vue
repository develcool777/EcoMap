<template>
<div class="hals">
  <div class="hals__sel">
    <select name="" id="" class="hals__select">
      <option value="EN" class="hals__option">EN</option>
      <option value="RU" class="hals__option">RU</option>
      <option value="UA" class="hals__option">UA</option>
    </select>
  </div>
  <svg class="hals__svg" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M8 8C6.88954 8 5.9433 7.61014 5.16129 6.83041C4.37928 6.05068 3.98827 5.10721 3.98827 4C3.98827 2.89279 4.37928 1.94932 5.16129 1.16959C5.9433 0.389864 6.88954 0 8 0C9.11046 0 10.0567 0.389864 10.8387 1.16959C11.6207 1.94932 12.0117 2.89279 12.0117 4C12.0117 5.10721 11.6207 6.05068 10.8387 6.83041C10.0567 7.61014 9.11046 8 8 8ZM8 10.0117C8.98534 10.0117 10.0723 10.152 11.261 10.4327C12.4497 10.7135 13.5367 11.1735 14.522 11.8129C15.5073 12.4522 16 13.1774 16 13.9883V16H0V13.9883C0 13.1774 0.492669 12.4522 1.47801 11.8129C2.46334 11.1735 3.55034 10.7135 4.739 10.4327C5.92766 10.152 7.01466 10.0117 8 10.0117Z" fill="#F2F2F2"/>
</svg>
<svg  class="hals__svg" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M7.03137 12.3046C8.42991 12.3046 9.77117 11.749 10.7601 10.7601C11.749 9.77117 12.3046 8.42991 12.3046 7.03137C12.3046 5.63283 11.749 4.29157 10.7601 3.30266C9.77117 2.31374 8.42991 1.75817 7.03137 1.75817C5.63283 1.75817 4.29158 2.31374 3.30266 3.30266C2.31374 4.29157 1.75817 5.63283 1.75817 7.03137C1.75817 8.42991 2.31374 9.77117 3.30266 10.7601C4.29158 11.749 5.63283 12.3046 7.03137 12.3046ZM12.5858 11.3431L15.7322 14.4894C15.816 14.5706 15.8829 14.6676 15.9289 14.7748C15.9749 14.8821 15.999 14.9974 16 15.1141C16.0009 15.2308 15.9786 15.3465 15.9343 15.4545C15.8901 15.5625 15.8247 15.6606 15.7421 15.743C15.6596 15.8255 15.5614 15.8907 15.4534 15.9348C15.3453 15.9789 15.2296 16.0011 15.1129 16C14.9962 15.9989 14.8809 15.9746 14.7737 15.9284C14.6665 15.8823 14.5696 15.8153 14.4886 15.7313L11.3422 12.5849C9.9294 13.6816 8.15175 14.1987 6.37113 14.0308C4.59051 13.863 2.94078 13.0229 1.75778 11.6815C0.574778 10.3401 -0.0525668 8.59834 0.00345308 6.81071C0.059473 5.02308 0.794647 3.32398 2.05931 2.05931C3.32398 0.794647 5.02308 0.059473 6.81071 0.00345308C8.59834 -0.0525668 10.3401 0.574778 11.6815 1.75778C13.0229 2.94078 13.863 4.59051 14.0308 6.37113C14.1987 8.15174 13.6816 9.9294 12.5849 11.3422L12.5858 11.3431Z" fill="#F2F2F2"/>
</svg>

</div>
</template>

<script>
export default {
  name: 'HeaderAccLanSer'
}
</script>
<style lang="scss">
.hals {
  @include FCenter(space-between);
  width: rem(125);
  &__sel {
    width: rem(50);
    position: relative;
  }
  &__sel:after {
    top: 50%;
    left: 70%;
    margin-top: rem(-2);
    position: absolute;
    cursor: pointer;
    pointer-events: none;
    content: "";
    width: 0;
    height: 0;
    display: block;
    border-style: solid;
    border-width: 5px 5px 0 5px;
    border-color: $white transparent transparent transparent;
  }
  &__select {
    cursor: pointer;
    width: 100%;
    outline: none;
    color: $white;
    font-size: rem(20);
    background: none;
    border: none;
    appearance: none;
  }
  svg path {
  fill:inherit;
  stroke:inherit;
  stroke-width:inherit;
  }
  &__svg {
    fill: $white;
    transition-duration: .5s;
  }
  &__svg:hover {
    cursor: pointer;
    fill:red;
  }
}
</style>
