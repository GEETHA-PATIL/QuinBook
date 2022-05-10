<template>
<div class="main">
    <!-- <div class="header">
        <div class="logo">
            <img src="@/assets/logo.jpg" alt="facebooklogo" height="40px" width="40px">
            <img src="@/assets/icons8-search-36.png" alt="search" height="20px" width="20px" id="s">
            <input type="search" name="op" placeholder="          Search Facebook">
        </div>
        <div class="elements">
            <img src="@/assets/home.svg" alt="home" @click.prevent="home">
            <img src="@/assets/watch.svg" alt="watch">
            <img src="@/assets/group.svg" alt="addFriend" @click.prevent="addfriend">
            <img src="@/assets/game.svg" alt="game">
        </div>
        <div class="login">
            <div class="info">
                <img src="@/assets/myimage.jpeg" class="picture" alt="christod">
                <text>G.V.S.Kumar</text>
            </div>
            <img src="@/assets/black_plus.jpg" height="40px" width="40px">
            <img src="@/assets/message.svg" height="30px" width="30px">
            <img src="@/assets/notification.svg" height="20px" width="20px">
        </div>
    </div> -->
    <NavBar />
    <div class="Body">
        <!-- <div class="left">
            <div class="profile">
                <img src="@/assets/myimage.jpeg" class="picture" alt="christod">
                G.V.S.KUMAR
            </div>
            <a href="https://www.covid19india.org/"><div class="elementstyling">
                <img src="@/assets/covid.png" alt="covid">
                COVID-19 Information Center
            </div></a>
            <div class="elementstyling">
                <img src="@/assets/page.png" alt="pages" @click.prevent="userBusiness">
                Pages
            </div>
            <div class="elementstyling" @click.prevent="getFriends">
                <img src="@/assets/friends.png" alt="Friends">
                Friends
            </div>
            <div class="elementstyling">
                <img src="@/assets/watch.png" alt="Watch">
                Watch
            </div>
            <a href="https://www.timeanddate.com/calendar/"><div class="elementstyling">
                <img src="@/assets/events.png" alt="Events">
                Events
            </div></a>
            <div class="elementstyling">
                <img src="@/assets/memories.png" alt="Memory">
                Memories
            </div>
            <div class="elementstyling">
                <img src="@/assets/saved.png" alt="Saved">
                Saved
            </div>
        </div> -->
        <div class="left">
            <LeftNavBar />
        </div>
        <div class="middle">
            <div class="what">
                <div class="whatsinmind">
                    <img :src="this.profileImage" alt="profilepic" class="picture" />
                    <input type="text" placeholder="What's on your mind ?" v-model="descrip" />
                    <button @click.prevent="posttext">Post</button>
                </div>
                <div>
                    <hr />
                </div>
                <div class="gallery">
                    <div class="galleryitem">
                        <img src="@/assets/video.svg" alt="livevideo" />
                        Live Video
                    </div>
                    <div class="galleryitems" @click.prevent="addPost">
                        <img src="@/assets/photo.svg" alt="photo" />
                        Photo
                    </div>
                    <div class="galleryitems">
                        <img src="@/assets/Smiley.jpg" alt="Feelings" height="25px" width="25px" />
                        Feeling/Activity
                    </div>
                </div>
            </div>
            <!-- <div class="profiles">
                <div class="galleryitems">
                    <img src="@/assets/live-video.jpg" alt="livevideo" height="25px" width="25px">
                    Create Room
                </div>
                <div>
                    <img src="@/assets/team-2.jpg" alt="team1" class="picture1">
                </div>
                <div>
                    <img src="@/assets/team-3.jpg" alt="team1" class="picture1">
                </div>
                <div>
                    <img src="@/assets/team-4.jpg" alt="team1" class="picture1">
                </div>
                <div>
                    <img src="@/assets/testimonials-1.jpg" alt="team1" class="picture1">
                </div>
                <div>
                    <img src="@/assets/testimonials-3.jpg" alt="team1" class="picture1">
                </div>
            </div> -->
            <div class="post" v-for="user in getPosts" :key="user">
                <div class="pic">
                    <div class="pleft">
                        <img :src="user.userImg" alt="team" class="picture" />
                        <div class="name">
                            <b>{{ user.userName }}</b>
                            <div class="time">
                                {{user.dateTime}}
                                <img src="privacy.JPG" alt="" />
                            </div>
                        </div>
                    </div>
                    <div class="pmiddile">
                        <div class="title">
                            <h1>{{user.title}}</h1>
                        </div>
                    </div>
                    <div class="pritght">
                        <img src="@/assets/menu.jpeg" alt="bar" class="picture1" />
                    </div>
                </div>
                <div v-if="user.userImg">
                    <img :src="user.image" alt="team1" height="400px" />
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

                        <p>view Comments</p>
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
            <!-- 
            <div class="post" v-for="user in getad" :key="user">
                <div class="name2">OFFERS ON</div>
                <div class="name1">
                    {{ user.title }}
                </div>
                <div class="pic">
                    <img :src="user.image" alt="team1" height="400px" width="700px" />
                </div>
            </div> -->
        </div>

        <!-- <div class="elementstyling" >
                <img src="@/assets/team-3.jpg" alt="team3" class="picture1">
                Jarib Farhan
            </div>
            <div class="elementstyling">
                <img src="@/assets/team-4.jpg" alt="team4" class="picture1">
                Rashid Shareef
            </div>
            <div class="elementstyling">
                <img src="@/assets/testimonials-1.jpg" alt="testimonials-1" class="picture1">
                Kamal Joardar
            </div>
            <div class="elementstyling">
                <img src="@/assets/testimonials-2.jpg" alt="testimonials-2" class="picture1">
                Bruce Pobi
            </div>
        </div> -->
    </div>
</div>
</template>

<script>
import NavBar from "./NavBar.vue";
import LeftNavBar from "./LeftNavBar.vue";
import Vue from "vue";
export default {
    name: "UserHome",
    components: {
        NavBar,
        LeftNavBar,
    },
    data() {
        return {
            userid: "",
            getad: [],
            getPosts: [],
            getComments: [],
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
        // this.axios
        //     .get(`http://10.20.2.212:8082/Ads/getAds?Username=${this.useremail}`)
        //     .then((resp) => {
        //         console.log(resp.data.data);
        //         this.getad = resp.data.data;
        //     });
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
                    }, {
                        headers: {
                            Authorization: "Bearer " + this.auth,
                        },
                    }
                ).then((result) => {
                    console.log("Result", result.data);
                });
        },
        viewComments(id) {
            this.axios
                .get(`http://localhost:8082/commentService/getAllComments/${id}`, {
                    headers: {
                        Authorization: `Bearer ${this.auth}`,
                    },
                })
                .then((resp) => {
                    console.log(resp.data.data);
                    this.getComments = resp.data;
                });
        }
    }
};
</script>

<style scoped>
/* comment section*/

.commentname{
    margin-left: 20px;
    color: blue;
    display: flex;
    flex-wrap: wrap;
padding: 2px;

}
.commenttitle{
margin-left: -390px;
margin-top: -23px;

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

.comment {
    margin-top: 3px;

    width: 25px;

    height: 25px;
}

.title {
    margin-left: -100px;
}

@media only screen and (max-device-width: 480px) {

    .elements {
        margin-right: -20px;
    }

    .logo {
        margin-left: -50px;
    }

    .middle {
        margin-left: 330px;
        margin-top: 20px;
    }

    body {
        /* padding: 10px; */
        margin-top: 20px;
    }

}
</style>
