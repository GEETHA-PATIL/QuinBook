<template>
<div class="main" :style="{
      background:
        'linear-gradient(to bottom, rgb(247, 247, 247), rgb(224, 224, 224)',
    }">
    <div class="header">
        <div class="header-left">
            <img class="header-left-img" src="@/assets/image2.png" alt="" width="50px" />
            <div class="header-input">
                <img src="@/assets/icons8-search-36.png" alt="" class="search-image" />
                <input type="text" placeholder="Search QuinBook" />
            </div>
        </div>

        <div class="header-middle">
            <div class="header-option active">
                <img src="@/assets/home.svg" alt="" @click.prevent="home" />
            </div>
            <div class="header-option">
                <img src="@/assets/watch.svg" alt="" @click.prevent="adds" />
            </div>
            <div class="header-option">
                <img src="@/assets/group.svg" alt="" @click.prevent="addfriend" />
            </div>
            <div class="header-option">
                <img src="@/assets/game.svg" alt="" />
            </div>
        </div>

        <div class="header-right">
            <div class="header-info">
                <img class="user-avatar" :src="this.profileImage" alt="" @click.prevent="profile" />
                <p>{{this.userName}}</p>
            </div>
            <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQtvaJEgRXWeZo0jcSbsilK4DTBlYs7Gvr3hRrG_wXoqG8maN9rNj_jJb3hldaWp7PzDOE&usqp=CAU" height="50px" width="50px" class="header-image" @click.prevent="addPost" />
            <div class="logout" @click="exit">
                <img src="data:image/png;base64,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" alt="" width="25px" height="25px" />
            </div>
        </div>
    </div>

    <div id="upper-profile">
        <div id="upper-profile-image">
            <img src="https://mobilemonkey.com/wp-content/uploads/2020/12/welcome-greeting-message.png" alt="" />
        </div>

        <div id="profile-d">
            <div id="profile-pic">
                <img :src="this.profileImage" alt="" />
            </div>

            <div id="u-name">{{this.userName}} {{this.lastName}}</div>

            <div id="privacy">
                <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ_rc2hGOB2BbXaYejAHn_H7N-tjxB2bgDAOA&usqp=CAU" alt="" />
                <span>Privacy</span>
            </div>
        </div>
    </div>

    <div class="main-section">
        <div class="left-section">
            <!-- <ul class="sidebar"> -->
            <div class="left-top-section">
                <div class="l-t-intro">
                    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTSQz9Jh7ZDbYf_ERvahYScUioB6fc0ZngxsP-Sio4T-_NGtRWnIDutEJ06J41tRiwpU0I&usqp=CAU" alt="" width="25px" height="25px" />

                    <span> Intro </span>
                    <div class="edit1">
                        <img src="@/assets/106-1067798_png-pencil-edit-logo-png-download-edit-icon-removebg-preview.png" width="22px" height="22px" alt="" @click="editProfile()" />
                    </div>
                </div>

                <div class="descr">
                    <p>{{this.userName}} {{this.lastName}}</p>
                    <p>{{this.email}}</p>
                    <p>{{this.phno}}</p>
                    <!-- <p>geetha.patil@Quinbay.com</p> -->
                    <!-- <p>9876543210</p> -->
                </div>
            </div>
            <!-- </ul> -->

            <div class="left-bottom">
                <div class="l-b-intro">
                    <img src="@/assets/photo.svg" alt="" width="30px" height="30px" />

                    <span> Photos </span>
                    <div class="edit">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSVfNkdMF5dpDxdEbksQ-hvrRQ-bIAfkjslWw0oAAUN718RdRaZogOjAeozE6dCCKnMwlQ&usqp=CAU" width="22px" height="22px" alt="" />
                    </div>
                </div>
                <div  class="l-b-images"  >
                    <div  v-for="user in getrequest" :key="user.id"  :v-if="user.image"  >
                        <img :src="user.image"  class="left-bottom-img" />
                    </div>
                </div>
            </div>
        </div>

        <div class="middle-section">
            <div class="first-section">
                <div class="upper-section">
                    <img :src="this.profileImage" class="main-img" />
                    <input type="text" placeholder="What's on your mind?" class="main-input" v-model="descrip" />
                    <button @click.prevent="posttext">POST</button>
                </div>
            </div>

            <div class="third-section">
                <div class="post" v-for="user in getrequest" :key="user">
                    <div class="post-top">
                        <img class="testimonals-image" :src="user.userImg" alt="" />

                        <div class="post-topInfo">
                            <h3 class="post-head">{{user.userName}}</h3>
                            <div class="post-details">
                                <p>{{user.dateTime}}</p>
                                <!-- <img src="@/assets/privacy.jpg" /> -->
                            </div>
                        </div>

                        <div>
                            <img src="https://toppng.com/uploads/preview/edit-delete-icon-delete-icon-11553444925vxge0bju5o.png" alt="" class="postrightop" width="100" height="20" @click="deletePost(user.id)" />
                        </div>
                    </div>

                    <div v-if="user.image" class="post-image">
                        <img :src="user.image" alt="Post" />
                    </div>
                    <div>
                        {{user.description}}
                    </div>
                    <div class="post-options">
                        <div class="post-option">
                            <img src="https://media.istockphoto.com/vectors/approved-or-thumbs-up-gray-color-like-icon-vector-id1248726867?k=20&m=1248726867&s=170667a&w=0&h=QNIorlpO3JDuwtxGtNY522Pkztu45WR3HBrbXLkkWD8=" />
                            <!-- <img src="https://www.clipartkey.com/mpngs/m/62-624598_x-clipart-thumb-blue-thumbs-up-icon.png" class="post-attributes" alt=""> -->
                            <p>Like</p>
                        </div>
                        <div class="post-option">
                            <img src="https://media.istockphoto.com/vectors/approved-or-thumbs-up-gray-color-like-icon-vector-id1248726867?k=20&m=1248726867&s=170667a&w=0&h=QNIorlpO3JDuwtxGtNY522Pkztu45WR3HBrbXLkkWD8=" class="dislike" />
                            <!-- <img src="https://www.clipartkey.com/mpngs/m/62-624598_x-clipart-thumb-blue-thumbs-up-icon.png" class="post-attributes" alt=""> -->
                            <p>Dislike</p>
                        </div>

                        <div class="post-option">
                            <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQWM5cdZS3Cd2_TfoPR3IvJBGiIaBeyX9VXKg&usqp=CAU" id="comment" />
                            <p @click="changeState" ref="toggle">Comment</p>
                        </div>

                        <div class="post-option">
                            <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQWM5cdZS3Cd2_TfoPR3IvJBGiIaBeyX9VXKg&usqp=CAU" alt="" class="comment" @click="viewComments(user.id)" />
                            <p>View Comments</p>
                        </div>
                    </div>
                    <div class="comments" id="comments" v-show="show">
                        <div v-for="comm in getComments" :key="comm">
                            <div class="commentname">
                                <div> <img :src="comm.userDp" alt="team" class="picture" /></div>
                                <div class="name">
                                    <b>{{ comm.userName }}</b>
                                </div>
                            </div>
                            <div class="commenttitle">

                                {{comm.comment}}

                            </div>
                        </div>
                        <div class="comment-text">
                            <textarea placeholder="Comment here...." spellcheck="false" v-model="comment" required></textarea>

                            <!-- <div class="submitcomment"> -->

                            <button class="btn-comment" type="submit" @click="postComment(user.id)" style="width: 100px; height: 50px">
                                Post
                            </button>

                            <!-- </div> -->
                            <!-- <button class="btn-view" @click="viewComments">View Comments</button> -->

                            <!-- </div> -->
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="right-section">
            <div class="r-t-heading">
                <img src="@/assets/friends.png" alt="">
                <span> Friends</span>
            </div>

            <ul>
                <div class="post" v-for="user in getFriends" :key="user">
                    <li class="right-ul">
                        <img :src="user.receiverImage" class="right-image" />
                        <p class="right-p">{{user.receiverName}}</p>
                    </li>
                </div>
                <!-- <li class="right-ul" v-for="user in getFriends" :key="user">
                    <img src="@/assets/team-2.jpg" class="right-image" />
                    <p class="right-p">{{user.receiverName}}</p>
                </li> -->
            </ul>
            <!-- <ul>
                <li class="right-ul">
                    <img src="@/assets/team-2.jpg" class="right-image" />
                    <p class="right-p">Sheikh Kalim</p>
                </li>
                <li class="right-ul">
                    <img src="@/assets/team-4.jpg" class="right-image" />
                    <p class="right-p">Jarib Farhan</p>
                </li>
                <li class="right-ul">
                    <img src="@/assets/team-3.jpg" class="right-image" />
                    <p class="right-p">Rashid Shareef</p>
                </li>
                <li class="right-ul">
                    <img src="@/assets/testimonials-1.jpg" class="right-image" />
                    <p class="right-p">Kamal Joardar</p>
                </li>
                <li class="right-ul">
                    <img src="@/assets/testimonials-2.jpg" class="right-image" />
                    <p class="right-p">Bruce Pobi</p>
                </li>
            </ul> -->
        </div>
    </div>
</div>
</template>

<script>
import swal from 'sweetalert';
// import Vue from "vue"
export default {

    name: "IndividualProfile",
    data() {
        return {
            userName: '',
            lastName:'',
            userId: '',
            profileImage: '',
            getrequest: [],
            getFriends: [],
            getComments: [],
            email: '',
            frienduserid: "",
            phno: '',
            descrip: '',
            show: false,
            comment: ""
        }
    },
    created() {
        this.frienduserid = JSON.parse(localStorage.getItem('userId'))
        this.axios.get(`http://localhost:8082/post/getPost/${this.frienduserid}`).then(resp => {
            console.log(resp.data.data)
            this.getrequest = resp.data
        })

        this.axios.get(`http://localhost:8082/user/getuser/${this.frienduserid}`)
            .then((resp) => {
                this.userId = resp.data.uid,
                    this.userName = resp.data.firstName,
                    this.lastName = resp.data.lastName,
                    this.profileImage = resp.data.profilePicture,
                    this.email = resp.data.email,
                    this.phno = resp.data.phno
            })
        this.handle()
    },

    methods: {
        // getUserName() {
        //     const userid = JSON.parse(localStorage.getItem('userId'))
        //     Vue.axios.get(`http://localhost:8082/user/userName/${userid}`, {
        //             headers: {
        //                 'Authorization': `Bearer ${this.auth}`,
        //             }
        //         })
        //         .then((resp) => {
        //             this.userName = resp.data.data;
        //         })
        // },
        addfriend() {
            this.$router.push("/AddFriends")
        },
        // getFriends() {
        //     this.$router.push("/FriendsLists")
        // },
        userBusiness() {
            this.$router.push("/UserBusinessPage")
        },
        home() {
            this.$router.push("/UserHome")
        },
        profile() {
            this.$router.push("/IndividualProfile")
        },
        exit() {
            sessionStorage.removeItem('Authorization')
            localStorage.removeItem('userId')
            this.$router.push("/")

        },
        addPost() {
            this.$router.push("/AddPost")
        },
        handle() {
            console.log("hello")

            this.axios.get(`http://localhost:8082/request/getAllFriends/${this.frienduserid}`).then(resp => {
                console.log(resp.data)
                this.getFriends = resp.data

            })
        },
        deletePost(postId) {
            this.axios.delete(`http://localhost:8082/post/deletePost/${postId}`).then(resp => {
                console.log(resp.data)
                // swal({
                //             title: "Post deleted",
                //             text: "",
                //             icon: "success",
                //             button: "OKAY",
                //             timer:"3000"

                //         })
                swal({
                    title: "Post Deleted",
                    text: "click",
                    button: "ok",
                    type: "success"
                }).then(function () {
                    location.reload();
                });
            })
        },
        editProfile() {
            this.$router.push('/EditProfile')
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

        postComment(userid1) {
            // this.i += 1

            console.log(" comment", this.comment);

            this.axios
                .post(
                    "http://localhost:8082/commentService/addComment", {
                        pid: userid1,
                        uid: this.userid,
                        comment: this.comment,
                        userName: this.userName,
                        userDp: this.profileImage
                    }
                ).then((result) => {
                    console.log("Result", result.data);
                });
        },
        viewComments(id) {
            this.axios
                .get(`http://localhost:8082/commentService/getAllComments/${id}`)
                .then((resp) => {
                    console.log(resp.data.data);
                    this.getComments = resp.data;
                });
        },
        adds() {
            this.$router.push("/AddsComponent");
        },
    }
};
</script>

<style scoped>
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

.commentname {
    margin-left: 20px;
    color: blue;
    display: flex;
    flex-wrap: wrap;
    padding: 2px;

}

.commenttitle {
    margin-left: -100px;
    margin-top: -23px;
    width: 500px;
    overflow: auto;
    font-size: 20px;
    font-family: 'Times New Roman', Times, serif;
    padding: 2px;
    font-weight: 500;
}

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

#upper-profile {
    /* position: relative; */
    position: static;
    display: flex;
    flex-wrap: wrap;
}

#upper-profile-image {
    height: 360px;
    width: 100%;

    overflow: hidden;
}

#upper-profile-image img {
    width: 100%;
    margin-top: -10%;
    z-index: 1;
}

#profile-d {
    display: flex;
    flex-direction: row;
}

#profile-pic {
    width: 180px;
    height: 160px;
    border-radius: 3px;
    margin-top: -120px;
    margin-left: 30px;
    box-shadow: 0 0 0 5px #fff;
}

#profile-pic img {
    width: 100%;
    height: 160px;
}

#u-name {
    /* color: #fff; */
    font-size: 36px;
    font-weight: bold;
    margin-top: -50px;
    margin-left: 20px;

}

#privacy {
    width: 100px;
    height: 30px;
    margin-top: -50px;
    margin-left: 800px;
    /* border: 1px solid black; */
    background: white;
    /* border-radius: 10px; */
    justify-content: space-between;
}

#privacy img {
    margin-left: 5px;
    margin-top: 2px;
    margin-right: 5px;

    width: 20px;
    height: 20px;
    background: #fff;
}

body {
    background: linear-gradient(to bottom,
            rgb(144, 92, 92),
            rgb(224, 224, 224));
}

/* Right Section */

.right-image {
    border-radius: 100%;
    height: 60px;
    width: 60px;
}

.right-ul {
    display: flex;
    align-items: center;
    width: 250px;
    padding-left: 20px;
    margin-bottom: 20px;
    cursor: pointer;
}

.right-p {
    margin-left: 15px;

}

.right-ul:hover {
    background-color: rgb(255, 255, 255);
    border-radius: 20px;
}

.right-section {
    line-height: 50px;
    padding-left: 30px;
    text-align: center;

    padding: auto;
}

.r-t-heading {
    display: flex;
    justify-content: center;
    background: #fff;
}

.r-t-heading img {
    margin-top: 12px;
    margin-right: 5px;
    height: 30px;
    width: 30px;
}

/* Middle section  */

.upper-section {
    display: flex;
    align-items: center;
}

.main-img {
    border-radius: 100%;
    height: 50px;
    width: 50px;
}

.main-input {
    width: 520px;
    font-size: 18px;
    background-color: rgb(240, 240, 240);
    border: none;
    border-radius: 20px;
    padding: 10px;
    margin-left: 15px;
    display: inline-block;
    /* float: right; */
}

.main-img-bottom {
    width: 30px;
    height: 30px;
}

#smiley {
    border-radius: 50%;
}

.main-text-bottom {
    font-size: 15px;
    margin-left: 10px;
    font-style: inherit;
}

.first-section {
    background-color: white;
    border-radius: 15px;
    padding: 14px;
}

.main-btn {
    border: none;
    border-radius: 10px;
    padding: 0 15px;
    display: flex;
    align-items: center;
    cursor: pointer;
}

.upper-btns {
    display: flex;
    justify-content: space-around;
}

.second-section {
    display: flex;
    align-items: center;
    background-color: #fff;
    border-radius: 20px;
    padding: 10px;
    margin-top: 20px;
    justify-content: space-evenly;
}

.testimonals-image {
    border-radius: 100%;
    width: 40px;
    height: 40px;
    margin: 0 10px;
    cursor: pointer;
}

.second-btn {
    border: none;
    border-radius: 10px;
    /* padding: 4px; */
    display: flex;
    align-items: center;
    cursor: pointer;
}

.second-text-bottom {
    font-size: 15px;
    margin-left: 10px;
}

.second-img-bottom {
    width: 30px;
    height: 20px;
}

/* Post section  */

.post {
    width: 100%;
    margin-top: 15px;
    border-radius: 15px;
    background-color: white;
    box-shadow: 0px 5px 7px -7px rgba(0, 0, 0, 0.75);
}

.post-image img {
    width: 100%;
    height: 32em;
}

.post-top {
    display: flex;
    position: relative;
    align-items: center;
}

.post-avatar {
    margin-right: 10px;
}

.post-topInfo {
    width: 80%;
}

.post-topInfo p {
    font-size: small;
    color: gray;
}

.post-bottom {
    margin-top: 10px;
    margin-bottom: 10px;
    padding: 15px 25px;
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

.post-option p {
    margin-left: 10px;
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

.post-option:hover {
    background-color: #eff2f5;
    border-radius: 10px;
}

.post-option img {
    width: 30px;
    height: 30px;
}

.post-details {
    display: flex;
    align-items: center;
}

.post-head {
    margin: 10px 0 0 0;
    font-size: 16px;
    color: rgb(75, 75, 179);
}

.postrightop {
    cursor: pointer;
    width: 20px;
}

.main-section {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    margin-top: 20px;
    margin-left: 20px;
    margin-right: 20px;

}

/* left section */

.left-section {
    width: 35%;
    padding-left: 20px;
    height: 680px;
}

.left-top-section {
    background: #fff;
    padding: 15px 15px 15px 15px;
}

.l-t-intro {
    display: flex;

}

.l-t-intro span,
.right-section span {
    position: relative;
    top: 2px;
    color: #707070;
    font-size: 18px;
    padding-left: 5px;
}

.edit1 {
    cursor: pointer;
    margin-left: 240px;

}

.edit {
    margin-left: 210px;
}

.descr {
    color: #797979;
    font-size: 15px;
    line-height: 1.3;
}

.left-bottom {
    padding: 2px;
    background: #fff;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    margin-top: 20px;
}
.l-b-images{
    display: flex;
    flex-wrap: wrap;
    width: 100%;
}

.l-b-intro {
    display: flex;
    padding: 20px 20px 10px;
}

.l-b-intro span {
    position: relative;
    top: 2px;
    color: #707070;
    font-size: 18px;
    padding-left: 5px;
}

.left-bottom-img {
    display: flex;
    flex-direction: row;
    margin-top: 1px;
    margin-right: 1px;
    width: 119px;
    height: 119px;

    
}

.middle-section {
    /* margin-left: 50px; */
    width: 40%;
    margin-left: 80px;
}

.right-section {
    width: 35%;
}

.header-left .header-left-img {
    height: 40px;
}

.user-avatar {
    border-radius: 50%;
    width: 45px;
    margin-right: 20px;
}

.header {
    display: flex;
    justify-content: space-between;
    position: sticky;
    background-color: white;
    z-index: 100;
    top: 0;
    box-shadow: 0 5px 8px -9px rgba(0, 0, 0, 0.75);
    padding: 10px 0;
}

@media only screen and (max-device-width: 350px) {
    .main {
        width: 1200px;
    }

    .header {
        display: flex;
        margin-left: 30px;
        width: 1120px;
    }

    .header-right {
        margin-left: 20px;
    }

    #upper-profile {
        width: 1100px;
        margin-left: 30px;
    }

    #privacy {
        margin-left: 560px;
    }

    .main-section {
        display: flex;
        flex-direction: column;
    }

    .left-section {
        width: 1100px;
    }

    .l-t-intro img,
    .l-b-intro img {
        margin-top: 10px;
    }

    .l-t-intro span,
    .l-b-intro span {
        font-size: 40px;
    }

    .descr {
        font-size: 35px;
    }

    .edit1 {
        margin-left: 950px;
    }

    .edit {
        margin-left: 920px;
    }

    .middle-section {
        margin-top: 750px;
        width: 1050px;
        margin-left: 35px;
    }

    .right-section {
        width: 950px;
    }

    .right-ul {
        margin-left: 300px;
        background: #fff;
        width: 500px;
    }

    .r-t-heading {
        margin-left: 270px;
    }

    .post-image img {
        height: 850px;
    }
}

/* for tablet screen */

@media only screen and (min-device-width: 350px) and (max-device-width: 800px) {
    .main {
        width: 1200px;
    }

    .header {
        display: flex;
        margin-left: 30px;
        width: 1168px;
    }

    #upper-profile {
        width: 1168px;

        margin-left: 30px;
    }

    #privacy {
        margin-left: 600px;
    }

    .main-section {
        display: flex;
        flex-direction: column;
    }

    .left-section {
        width: 1150px;
    }

    .edit1 {
        margin-left: 950px;
    }

    .edit {
        margin-left: 920px;
    }

    .l-t-intro img,
    .l-b-intro img {
        margin-top: 10px;
    }

    .l-t-intro span,
    .l-b-intro span {
        font-size: 35px;
    }

    .descr {
        font-size: 32px;
    }

    .middle-section {
        margin-top: 800px;
        width: 1125px;
        margin-left: 32px;
    }

    .right-section {
        width: 950px;
    }

    .right-ul {
        margin-left: 300px;
        background: #fff;
        width: 500px;
    }

    .r-t-heading {
        margin-left: 270px;
    }

    .post-image img {
        height: 850px;
    }
}

.header-left {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
}

.header-input {
    display: flex;
    align-items: center;
    background-color: #eff2f5;
    padding: 10px;
    margin-left: 10px;
    border-radius: 999px;
}

.header-input input {
    border: none;
    background-color: transparent;
    outline-width: 0;
}

.header-middle {
    display: flex;
    flex: 1;
    justify-content: center;
}

.header-option {
    display: flex;
    align-items: center;
    padding: 0 30px;
    cursor: pointer;
}

/* .header-option.active {
     border-bottom: 4px solid #2e81f4; 
  } */

.header-option:hover {
    background-color: #eff2f5;
    border-radius: 10px;
    align-items: center;
    padding: 0 30px;
    border-bottom: none;
    border-bottom: 4px solid #2e81f4;
}

.header-info {
    display: flex;
    align-items: center;
}

.header-right {
    display: flex;
    align-items: center;
    width: 22%;
    float: right;
}

.header-image {
    width: 25px;
    height: 25px;
    margin: 0 15px;
    cursor: pointer;
}

.images {
    display: flex;
    flex-direction: row;
}

.search-image {
    width: 25px;
    height: 25px;
}
</style>
