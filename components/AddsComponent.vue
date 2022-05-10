<template>
<div class="main">
    <NavBar />
    <div class="Body">
        <div class="left">
            <LeftNavBar />
        </div>
        <div class="middle">
            <div class="post" v-for="user in getad" :key="user">
                <!-- <div class="name2">OFFERS ON</div> -->
                <div class="name1">
                    {{ user.title }}
                </div>
                <div class="pic">
                    <img :src="user.image" alt="team1" height="400px" width="700px" />
                </div>
            </div>
        </div>
    </div>
   
</div>
</template>

<script>
import NavBar from "./NavBar.vue";
import LeftNavBar from "./LeftNavBar.vue";
import Vue from "vue";
export default {
    name: "AddsComponent",
    components: {
        NavBar,
        LeftNavBar,
    },
    data() {
        return {
            userid: "",
            getad: [],
            getPosts: [],
            userName: "",
            useremail: "",
            profileImage: "",
            show: false,
            comment: "",
            descrip: '',
            i: 0,
        };
    },
    created() {
        this.userid = JSON.parse(localStorage.getItem("userId"));
        this.useremail = JSON.parse(localStorage.getItem("userEmail"));
        this.axios
            .get(`http://10.20.2.212:8082/Ads/getAds?Username=${this.useremail}`)
            .then((resp) => {
                console.log(resp.data.data);
                this.getad = resp.data.data;
            });
        this.axios
            .get(`http://localhost:8082/post/getFriendsPosts/${this.userid}`)
            .then((resp) => {
                console.log(resp.data.data);
                this.getPosts = resp.data;
            });

        this.axios
            .get(`http://localhost:8082/user/getuser/${this.userid}`)
            .then((resp) => {
                (this.userId = resp.data.uid),
                (this.userName = resp.data.firstName),
                (this.profileImage = resp.data.profilePicture);
            });

        this.handlerequest();
        this.getUserName();
    },
    methods: {
        addfriend() {
            this.$router.push("/AddFriends");
        },
        getFriends() {
            this.$router.push("/FriendsLists");
        },
        userBusiness() {
            this.$router.push("/UserBusinessPage");
        },
        home() {
            this.$router.push("/UserHome");
        },
        handlerequest() {
            this.axios
                .get(`http://localhost:8082/request/getAllFriends/${this.userid}`)
                .then((resp) => {
                    console.log(resp.data);
                    this.getrequest = resp.data;
                });
        },
        addPost() {
            this.$router.push("/AddPost");
        },
        getUserName() {
            const userid = JSON.parse(localStorage.getItem("userId"));
            Vue.axios
                .get(`http://localhost:8082/user/userName/${userid}`)
                .then((resp) => {
                    this.userName = resp.data;
                });
        },
        posttext() {
            this.axios.post(`http://localhost:8082/post/addPost`, {
                userName: this.userName,
                userImg: this.profileImage,
                userID: this.userId,
                description: this.descrip,
                image: "",
                title: "text"

            })
        },
        changeState: function () {
            this.show = !this.show;

            // this.$refs.toggle.innerText = this.show ? "Comment" : "Comment";
        },

        postComment() {
            // this.i += 1

            console.log(" comment", this.comment);

            Vue.axios
                .post(
                    "http://localhost:8082/commentService/save", {
                        comment: this.comment,
                    }
                )

                .then((result) => {
                    console.log("Result", result);
                });
        },
    },
};
</script>

<style scoped>
/* comment section*/
.btn-comment {
    background: #28f5e4;

    border-radius: 10px;

    border: none;

    margin-bottom: 15px;
}

.submitcomment {
    text-align: center;

    margin-right: 45px;
}

textarea {
    width: 70%;

    height: 43px;

    margin-bottom: 10px;
}

.comment-text {
    display: flex;

    margin-left: 40px;

    justify-content: space-evenly;
}

.header {
    display: flex;
    flex-wrap: wrap;
    /* margin-top: 10px; */
    gap: 80px;
    background-color: white;
    padding: 10px;
    transition: 1s;
    position: fixed;
    width: 100%;
}

#s {
    position: absolute;
    left: 75px;
    top: 20px;
}

.header .logo input {
    background-color: rgb(231, 229, 229);
    border: 1px solid white;
    border-radius: 30px;
    width: 250px;
}

.logo {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}

.logo form {
    margin-top: 10px;
}

.elements {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    width: 40%;
}

.login {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    width: 23%;
}

.info {
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
    align-items: center;
}

.picture {
    border-radius: 50%;
    height: 30px;
    width: 30px;
    transition: 2s;
}

.picture1 {
    border-radius: 50%;
    height: 40px;
    width: 40px;
    transition: 2s;
}

.main {
    /* background-color: rgb(231, 229, 229); */
    background-image: linear-gradient(to top,
            rgba(243, 239, 239, 0),
            rgb(206, 233, 247));

    scroll-behavior: auto;
}

.Body {
    display: flex;
    flex-flow: row wrap;
    flex-direction: row;
    gap: 13%;
    flex-wrap: wrap;
    padding: 40px 0 0 0;
}

.left {
    display: flex;
    flex-flow: column wrap;
    flex-direction: column;
    justify-content: left;
    position: fixed;
    gap: 20px;
}

.profile {
    cursor: pointer;
    margin-top: 35px;
    margin-left: 15px;
    align-items: center;
    display: flex;
    gap: 10px;
}

.profile:hover {
    background-image: white;
}

.elementstyling {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-left: 10px;
    cursor: pointer;
}

.middle {
    display: flex;
    flex-wrap: wrap;
    flex-flow: column;
    flex-direction: column;
    justify-content: left;
    gap: 5%;
    margin: 0 0 0 450px;
    scroll-behavior: smooth;
}

.what {
    display: flex;
    flex-wrap: wrap;
    flex-flow: column;
    flex-direction: column;
    justify-content: left;
    margin-top: 25px;
    border: 1px solid white;
    border-radius: 5px;
    background-color: white;
    padding: 10px;
}

.whatsinmind {
    display: flex;
    flex-wrap: wrap;
    flex-flow: row;
    flex-direction: row;
    align-items: center;
    gap: 20px;
}

.whatsinmind input {
    width: 450px;
    background-color: rgb(231, 229, 229);
    border: 1px solid white;
    border-radius: 20px;
    height: 0.5cm;
    padding: 10px;
}

.gallery {
    display: flex;
    flex-wrap: wrap;
    flex-flow: row;
    flex-direction: row;
    align-items: center;
    gap: 40px;
}

.galleryitems {
    display: flex;
    flex-wrap: wrap;
    flex-flow: row;
    flex-direction: row;
    align-items: center;
    background-color: rgb(231, 229, 229);
    border: 1px solid rgb(231, 229, 229);
    border-radius: 10px;
    padding: 5px;
    gap: 5px;
    cursor: pointer;
}

.galleryitem {
    margin-left: 20px;
    display: flex;
    flex-wrap: wrap;
    flex-flow: row;
    flex-direction: row;
    align-items: center;
    background-color: rgb(231, 229, 229);
    border: 1px solid rgb(231, 229, 229);
    border-radius: 10px;
    padding: 5px;
    gap: 5px;
}

hr {
    color: rgb(231, 229, 229);
}

.profiles {
    display: flex;
    flex-wrap: wrap;
    flex-flow: row;
    flex-direction: row;
    justify-content: left;
    border: 1px solid white;
    border-radius: 5px;
    background-color: white;
    padding: 10px;
    gap: 40px;
    margin-top: 20px;
}

.post {
    display: flex;
    flex-wrap: column wrap;
    flex-direction: column;
    justify-content: left;
    background-color: white;
    border: 1px solid white;
    border-radius: 5px;
    margin-top: 20px;
}

.pic {
    display: flex;
    flex-wrap: row wrap;
    flex-direction: row;
    justify-content: row;
    justify-content: space-between;
    padding-left: 10px;
    padding-top: 10px;
}

.pleft {
    display: flex;
    flex-wrap: row wrap;
    justify-content: row;
    justify-content: row;
    gap: 10px;
}

.name {
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    justify-content: column;
}

.name1 {
    font-weight: bold;
    font-size: 20px;
    font-family: "Times New Roman", Times, serif;
}

.name2 {
    font-weight: bold;
    font-size: 30px;
    font-family: "Times New Roman", Times, serif;
}

.time {
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    align-items: center;
}

.right {
    display: flex;
    flex-wrap: column wrap;
    flex-direction: column;
    justify-content: left;
    position: fixed;
    gap: 35px;
    margin-left: 1150px;
}

.elementstyling:hover {
    background-color: white;
}

.elements img:hover {
    background-color: blue;
}

.picture:hover {
    width: 50px;
    height: 50px;
}

.picture1:hover {
    width: 50px;
    height: 50px;
}

.header img:hover {
    width: 50px;
    height: 50px;
}

.header .login input:hover {
    width: 50px;
    height: 50px;
}

.header .elements input:hover {
    width: 50px;
    height: 50px;
}

a {
    text-decoration: none;
    color: black;
}

.post-options {
    border-top: 1px solid lightgray;

    display: flex;

    justify-content: space-evenly;

    font-size: medium;

    color: gray;

    cursor: pointer;
}

.post-option {
    display: flex;

    align-items: center;

    justify-content: center;

    padding: 5px;

    flex: 1;
}

.post-option img {
    width: 30px;

    height: 30px;
}

.post-option p {
    margin-left: 10px;
}

.post-option:hover {
    background-color: #eff2f5;

    border-radius: 10px;
}

.dislike {
    /* transform: (180); */

    margin-top: 10px;

    transform: rotate(180deg);
}

#comment {
    margin-top: 3px;

    width: 25px;

    height: 25px;
}

.title {
    margin-left: -100px;
}
</style>
