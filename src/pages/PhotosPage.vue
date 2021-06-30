<template>
  <v-container>
    <PhotoForm @addPhoto="addPhoto" />
    <v-row>
      <Photo
        v-for="photo in photos"
        :photo="photo"
        :key="photo.id"
        @openPhoto="openPhoto"
      />
    </v-row>
    <PhotoDialog :photo="selectedPhoto" v-model="dialogVisible" />
  </v-container>
</template>

<script>
import Photo from "../components/photo/Photo";
import PhotoForm from "../components/photo/PhotoForm";
import PhotoDialog from "../components/photo/PhotoDialog";
export default {
  components: { PhotoDialog, PhotoForm, Photo },
  data: () => {
    return {
      photos: [],
      selectedPhoto: {},
      dialogVisible: false
    };
  },
  mounted() {
    this.fetchTodo();
  },
  methods: {
    fetchTodo() {
      this.axios
        .get("https://jsonplaceholder.typicode.com/photos?_limit=10")
        .then(response => (this.photos = response.data));
    },
    addPhoto(photo) {
      this.photos.push(photo);
    },
    openPhoto(photo) {
      this.selectedPhoto = photo;
      this.dialogVisible = true;
    }
  }
};
</script>

<style scoped></style>">
