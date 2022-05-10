<template>
<body>
    <div class="container">
        <section class="post">
            <header>Create Post</header>
            <form action="" enctype="multipart/form-data" class="whole">
                <div class="content">
                    <img src="@/assets/image2.png" alt="logo" />
                    <div class="details">
                        <p>{{this.userName}}</p>
                        <div class="privacy">
                            <img src="@/assets/1835695-removebg-preview.png" alt="" />
                            <span>Friends</span>
                        </div>
                    </div>
                </div>

                <textarea placeholder="What's on your mind ?" spellcheck="false" v-model="description" required>
          </textarea>
                <div class="theme-emoji">
                    <!-- <img src="@/assets/icons/theme.svg" alt="theme" /> -->
                    <!--<div class="image">
              <div v-if="!image">
                <h2>Select an image</h2>
                <label for="">
                  <input
                    type="file"
                    id="file"
                    ref="file"
                    v-on:change="handleFileUpload()"
                  />
                </label>
                <button v-on:click="submitFile()">Submit</button>
              </div>
               <div v-else>
                <img :src="image" />
                <button @click="removeImage">Remove image</button>
              </div> 
            </div>-->

                    <label for="">
                        <div class="post_image">

                            <img class="imagesource" src="@/assets/icons/gallery.svg" />
                            <label class="labelimage">Enter an image url</label>
                            Enter title<input type="text" placeholder="  Enter title " v-model="title" />
                            <input type="text" id="file" placeholder="Enter Url" v-model="imageUrl" />
                        </div>
                    </label>
                    <!-- <div v-on:click="submitFile()">Submit</div> -->

                    <!-- <img src="@/assets/icons/smile.svg" alt="smile" /> -->
                </div>
                <!-- <div class="options">
            <p>Add to Your Post</p>
            <ul class="list">
              <li>
                <div class="image-upload">
                  <label for="file" class="image-uploads"
                    ><img src="@/assets/icons/gallery.svg" /></label
                  ><input id="file" type="file" />
                </div>
              </li>

              <li>
                <img src="@/assets/icons/tag.svg" alt="gallery" />
              </li>

              <li><img src="@/assets/icons/emoji.svg" alt="gallery" /></li>
              <li><img src="@/assets/icons/mic.svg" alt="gallery" /></li>
              <li><img src="@/assets/icons/more.svg" alt="gallery" /></li>
            </ul>
          </div> -->
                <router-link :to="{name:'IndividualProfile'}">
                  <button v-on:click="submitFile()">Post</button>
                </router-link> 
            </form>
        </section>
    </div>
</body>
</template>

<script>
export default {
    name: "AddPost",

    data() {
        return {

            description: "",
            image: "",
            userId: '',
            userName: '',
            profileImage: '',
            imageUrl: '',
            title: '',
        };
    },
    created() {
        this.getDetails();
    },

    methods: {
        removeImage: function () {
            this.image = "";
        },
        submitFile() {
            this.axios.post(`http://localhost:8082/post/addPost`, {
                    userName: this.userName,
                    userImg: this.profileImage,
                    userID: this.userId,
                    description: this.description,
                    image: this.imageUrl,
                    title: this.title

                }, 
                    this.$router.push('/IndividualProfile')
                )
                .then((result) => {
                    console.log("Result", result)

                    this.$router.push('/IndividualProfile')
                    console.log("Result", result)
                })
                    // this.$router.push('/IndividualProfile')
                    this.$router.go()


        },
        getDetails() {
            const userid = JSON.parse(localStorage.getItem('userId'))
            this.axios.get(`http://localhost:8082/user/getuser/${userid}`)
                .then((resp) => {
                    this.userId = resp.data.uid,
                        this.userName = resp.data.firstName,
                        this.profileImage = resp.data.profilePicture
                })
        }

        // addPost(){
        //   console.log("hello")
        //   this.axios.post(`http://10.20.2.195:8083/postService/save`,{
        //     description : this.description,
        //     image:this.image
        //   })
        //   .then((result)=>{
        //         console.log("Result",result)
        // })

        // }
        // addPost() {
        //   const formData = new FormData();
        //   formData.append("imagesArray", this.imagesArray, this.imagesArray.name);
        //   axios
        //     .post(`http://localhost:8083/postService/save`, formData)
        //     .then((response) => {
        //       console.log(response);
        //     });
        // },
    },
};
</script>

<style scoped>
.imagesource {
    margin-left: 130px;
    margin-bottom: -8px;
    /* padding-top: 10px; */
}

.labelimage {
    /* text-align: center; */
    margin-left: 5px;

}

.whole {
    /* height: fit-content; */
    height: 1000px;
}

.image-upload>input {
    display: none;
}

.image-uploads>input {
    display: none;
}

/* Import Google Font - Poppins */
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap");

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Poppins", sans-serif;
}

body {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    background: linear-gradient(#c4e6f0, #8dd7ee, #52cef0);
}

::selection {
    color: #fff;
    background: #3d8cec;
}

.container {
    display: flex;

    width: 500px;
    height: 500px;
    overflow: hidden;
    background: #fff;
    border-radius: 10px;
    transition: height 0.2s ease;
    box-shadow: 0 12px 28px rgba(0, 0, 0, 0.12);
}

.container.active {
    height: 590px;
}

.container section {
    width: 500px;
    background: #fff;
}

.container img {
    cursor: pointer;
}

.container .post {
    transition: margin-left 0.18s ease;
}

.container.active .post {
    margin-left: -500px;
}
@media only screen and  (max-device-width: 350px){
  body{
    width: 1100px;
    height: 800px;
    padding: 20px;
    margin-left: 40px;
  }
  .container{
    height: 550px;
  }
}

/* for tablet screen*/
@media only screen  and  (min-device-width: 350px)and  (max-device-width: 850px){
  body{
    width: 1100px;
    padding: 20px;
    margin-left: 40px;
  }
}

.post header {
    font-size: 22px;
    font-weight: 600;
    padding: 17px 0;
    text-align: center;
    border-bottom: 1px solid #bfbfbf;
}

.post form {
    margin: 20px 25px;
}

.post form .content {
    display: flex;
    align-items: center;
}

.post form .content img {
    cursor: default;
    max-width: 52px;
}

.post form .content .details {
    margin: -3px 0 0 12px;
}

form .content .details p {
    font-size: 17px;
    font-weight: 500;
}

.content .details .privacy {
    display: flex;
    height: 25px;
    cursor: pointer;
    padding: 0 10px;
    font-size: 11px;
    margin-top: 3px;
    border-radius: 5px;
    align-items: center;
    max-width: 98px;
    background: #e4e6eb;
    justify-content: space-between;
}

.details .privacy span {
    font-size: 13px;
    margin-top: 1px;
    font-weight: 500;
}

.privacy img {
    width: 15px;
    height: 15px;
}

.details .privacy i:last-child {
    font-size: 13px;
    margin-left: 1px;
}

form :where(textarea, button) {
    width: 100%;
    outline: none;
    border: none;
}

form textarea {
    resize: none;
    font-size: 18px;
    margin-top: 30px;
    min-height: 100px;
}

form textarea::placeholder {
    color: #858585;
}

form textarea:focus::placeholder {
    color: #b3b3b3;
}

form :where(.theme-emoji, .options) {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.theme-emoji img:last-child {
    max-width: 24px;
}

form .options {
    height: 57px;
    margin: 15px 0;
    padding: 0 15px;
    border-radius: 7px;
    border: 1px solid #b9b9b9;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}

form .options :where(.list, li) {
    display: flex;
    align-items: center;
    justify-content: center;
}

form .options p {
    color: #595959;
    font-size: 15px;
    font-weight: 500;
    cursor: default;
}

form .options .list {
    list-style: none;
}

.options .list li {
    height: 42px;
    width: 42px;
    margin: 0 -1px;
    cursor: pointer;
    border-radius: 50%;
}

.options .list li:hover {
    background: #f0f1f4;
}

.options .list li img {
    width: 23px;
}

form button {
    height: 53px;
    color: #fff;
    font-size: 18px;
    font-weight: 500;
    cursor: pointer;
    color: #bcc0c4;
    cursor: no-drop;
    border-radius: 7px;
    background: #e2e5e9;
    transition: all 0.3s ease;
}

form textarea:valid~button {
    color: #fff;
    cursor: pointer;
    background: #4599ff;
}

form #imagefile:valid~button {
    color: #fff;
    cursor: pointer;
    background: #4599ff;
}

form textarea:valid~button:hover {
    background: #1a81ff;
}

#imagefile:valid~button:hover {
    background: #1a81ff;
}

.container.active {
    opacity: 1;
}

.list li .column .details p {
    font-weight: 500;
}

.list li .column .details span {
    font-size: 14px;
    color: #65676b;
}

.list li .radio {
    height: 20px;
    width: 20px;
    border-radius: 50%;
    position: relative;
    border: 1px solid #707070;
}

.list li.active .radio {
    border: 2px solid #4599ff;
}

.list li .radio::before {
    content: "";
    width: 12px;
    height: 12px;
    border-radius: inherit;
}

.list li.active .radio::before {
    background: #4599ff;
}

.post1 {
    width: 100px;
    height: 100px;
    margin: auto;
    display: block;
    margin-top: -150px;
    margin-bottom: 10px;
}

.poooost {
    margin-top: 160px;
}

.post_image {
    margin-top: 100px;
}
</style>

  <!-- <div v-if="!image">
                  <h2>Select an image</h2>
                  <input type="file" @change="onFileChange" />
                </div>
                <div v-else>
                  <img :src="image" />
                  <button @click="removeImage">Remove image</button>
                </div> 

                 <div class="image-upload">
                  <label for="file-input" class="image-uploads"
                    ><img src="@/assets/icons/gallery.svg" /></label
                  ><input id="file-input" type="file" />
                </div>
                
                
                
                
                
                
                -->
