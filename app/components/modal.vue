<template lang="pug">
.modal-mask(@click='close', v-show='currentModal', transition='modal')
  .modal-area
    .modal-container(@click.stop='')
      component(:is='currentModal')

</template>

<script>
module.exports = {
  name: 'modal',
  store: ['currentModal', 'modalConfig'],
  methods: {
    close: function () {
      this.currentModal = undefined
      radio.$emit('modalClosed')
    }
  },
  mounted: function () {
    // When escape key is pressed close the modal
    document.addEventListener("keydown", (e) => {
      if (this.currentModal && e.keyCode == 27) {
        this.currentModal = undefined
        radio.$emit('modalClosed')
      }
    })
  }
}
</script>

<style lang="stylus">
  .modal-mask
    position fixed
    z-index 9998
    top 0
    left 0
    width 100%
    height 100%
    background-color rgba(0, 0, 0, .5)
    transition opacity .3s ease

  .modal-area
    position absolute
    top 10px
    bottom 10px
    left 40px
    right 40px

  .modal-container
    width 100%
    max-height 88%
    overflow-y scroll
    margin 40px auto 0
    background-color #fff
    border-radius 2px
    box-shadow 0 2px 8px rgba(0, 0, 0, .33)
    transition all .3s ease
    font-family Helvetica, Arial, sans-serif
    overflow-x hidden

  .modal-header h3
    margin-top 0
    color #42b983

  .modal-body
    margin 20px 0

  .text-right
    text-align right

  .form-label
    display block
    margin-bottom 1em
    & > .form-control
      margin-top 0.5em

  .form-control
    display block
    width 100%
    padding 0.5em 1em
    line-height 1.5
    border 1px solid #ddd

  .modal-enter, .modal-leave
    opacity 0

  .modal-enter .modal-container,
  .modal-leave .modal-container
    -webkit-transform scale(1.1)
    transform scale(1.1)

</style>