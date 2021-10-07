<template>
  <div class="container">
    <div>
      <input
        id="file-input"
        type="file"
        ref="fileInput"
        accept="image/*"
        @change="onFilePicked"
        required
      />
      <cld-image
        public-id="content/Bmvp (1)"
        width="200"
        crop="scale"
        fetchFormat="auto"
        quality="auto"
        loading="lazy"
      />

      <cld-image public-id="content/Bmvp (1)">
        <cld-transformation
          width="200"
          crop="scale"
          radius="max"
          fetchFormat="auto"
          quality="auto"
          loading="lazy"
          border="3px_solid_rgb:9ACD32"
        />
      </cld-image>
      <button @click="cloudinary">Upload</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        imageName: "",
        image: null,
        imageUrl: ""
      }
    };
  },
  methods: {
    cloudinary() {
      this.$cloudinary
        .upload(this.formData.imageUrl, {
          public_id: this.formData.imageName,
          folder: "content",
          upload_preset: "gurpobn6"
        })
        .then(res => console.log(res))
        .catch(err => cosole.log(err));
    },
    onFilePicked(event) {
      const files = event.target.files;
      const fileReader = new FileReader();
      fileReader.addEventListener("load", () => {
        this.formData.imageUrl = fileReader.result;
        console.log(this.formData.imageUrl);
      });
      fileReader.readAsDataURL(files[0]);
      const fileName = this.$refs.fileInput.value;
      this.formData.imageName = fileName
        .split("\\")
        .pop()
        .replace(/\.[^/.]+$/, "");
    }
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
