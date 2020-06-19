<template>
  <b-navbar type="is-black" :mobile-burger="false">
    <template slot="brand">
      <b-navbar-item>
        <span class="title" style="margin-right: 4px;">
          <img src="@/assets/logo.png" alt="🤖" class="logo"/>
        </span>
        <span class="title has-text-primary">
          StickerSnap
        </span>
        <span class="subtitle has-text-primary is-7" style="padding-bottom: 16px">
          The AI Sticker Maker
        </span>     
      </b-navbar-item>
    </template>
  </b-navbar>
</template>

<style scoped>
.logo {
    -webkit-filter: drop-shadow( 1px  1px 0 white) 
                    drop-shadow( 1px -1px 0 white) 
                    drop-shadow(-1px  1px 0 white) 
                    drop-shadow(-1px -1px 0 white);
    filter: drop-shadow( 1px  1px 0 white) 
            drop-shadow( 1px -1px 0 white)
            drop-shadow(-1px  1px 0 white) 
            drop-shadow(-1px -1px 0 white);
}
</style>