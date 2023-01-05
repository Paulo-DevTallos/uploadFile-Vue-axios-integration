<template>
  <div>
    <input type="file" @change="setFileOnChange" name="image" ref="file"/>
  </div>
  <RouterView />
</template>

<script>
import axios from 'axios'

export default {
  name: "App",
  data() {
    return {
      fileList: [],
    };
  },
  methods: {
    setFileOnChange() {
      this.fileList = this.$refs.file.files
      console.log(this.fileList)
      const formData = new FormData()

      formData.append('image', this.fileList[0])

      axios.post('http://localhost:3004/api/upload', formData, {
        headers: {
          "Content-Type": "multipart/form-data"
        }
      }).then(res => {
        console.log(res.data)
      })
    }
  },
  mounted() {
  },
};
</script>

<style scoped></style>
