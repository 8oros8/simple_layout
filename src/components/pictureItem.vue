<template>
  <div class="pictureItem">
    <div class="pictureItem__userWrapper">
      <img class="pictureItem__userProfileImage" :src="photoData.user.profile_image.small" alt="profile image">
      <div class="pictureItem__userInfo"
           @click="visitUser">
        <div class="pictureItem__userFullname">{{ photoData.user.first_name}}</div>
        <div class="pictureItem__username"> @{{ photoData.user.username }}</div>
      </div>
    </div>
    <img class="pictureItem__img" :src="photoData.urls.regular" :alt="photoData.alt_description">
    <div class="pictureItem__views">{{ photoData.likes }}<img class="pictureItem__eyeIcon" src="src/assets/images/eye.png" alt="eye image"></div>
  </div>
</template>

<script>
export default {
  name: "pictureItem",
  props: {
    photoData: Object,
  },
  methods: {
    visitUser() {
      window.location.href = this.photoData.user.links.html
    }
  }
}
</script>

<style lang="scss" scoped>
@import "src/assets/base.scss";

.pictureItem {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
  height: 304px;
  margin-bottom: 16px;
  @include _480 {
    height: 380px;
    max-width: 440px;
  }
  @include _768 {
    width: 45%;
    max-width: 320px;
    height: 312px;
  }
  @include _1000 {
    width: 45%;
    max-width: 320px;
    height: 312px;
  }
}
.pictureItem__userWrapper {
  display: flex;
  padding: 10px;
}
.pictureItem__userProfileImage {
  display: flex;
  width: 30px;
  height: 30px;
  border-radius: 50%;
}
.pictureItem__userInfo {
  display: flex;
  flex-direction: column;
  margin-left: 10px;
}
.pictureItem__userFullname {
  cursor: pointer;
  font-family: "Roboto Condensed", sans-serif;
  font-weight: 700;
  font-size: 12px;
  line-height: 14px;
  color: #333333;
}
.pictureItem__username {
  cursor: pointer;
  font-family: "Roboto Condensed", sans-serif;
  font-weight: 400;
  font-size: 12px;
  line-height: 14px;
  color: #8D8D8D;
}
.pictureItem__img {
  width: 100%;
  height: 230px;
  @include _480 {
    height: 300px;
    max-width: 440px;
  }
}
.pictureItem__views {
  display: flex;
  align-items: center;
  justify-content: right;
  padding: 10px;
  font-family: "Roboto Condensed", sans-serif;
  font-weight: 700;
  font-size: 12px;
  line-height: 14px;
  color: #8D8D8D;
}
.pictureItem__eyeIcon {
  width: 18px;
  height: 12px;
  margin-left: 5px;
}
</style>