<template>
<div class="main">
    <div class="header">
        <div class="logo">
            <img src="@/assets/image2.png" alt="facebooklogo" height="40px" width="40px" />
            <!-- <img src="@/assets/icons8-search-36.png" alt="search" height="20px" width="20px" id="s"> -->
            <input class="search_bar" type="search" name="op" v-model="searchQuery" placeholder="          Search QuinBook" />

            <button class="search_btn">
                <img @click="getData(searchQuery)" src="@/assets/icons8-search-36.png" alt="search" height="20px" width="20px" class="s" />
            </button>
        </div>
        <div class="elements">
            <img src="@/assets/home.svg" alt="home" @click.prevent="home" />
            <img src="@/assets/watch.svg" alt="watch" @click.prevent="adds" />
            <img src="@/assets/group.svg" alt="addFriend" @click.prevent="addfriend" />
            <a href="https://supermarioplay.com/"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ8hhI0z-r00gjhA28pSy0opFyL56TSAbGgSW4mBerPgAXFuYeVkwuI0a2UCUn2BFvXF8M&usqp=CAU" height="35px" width="35px" alt="game" /></a>
        </div>
        <div class="login">
            <div class="info">
                <img :src="this.profileImage" class="picture" alt="christod" @click.prevent="profile" />
                <!-- <p>{{this.data.userName}}</p> -->
                {{ userName }}
            </div>
            <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQtvaJEgRXWeZo0jcSbsilK4DTBlYs7Gvr3hRrG_wXoqG8maN9rNj_jJb3hldaWp7PzDOE&usqp=CAU" height="40px" width="40px" @click.prevent="addPost" />
            <div class="logout" @click="exit">
                <img src="data:image/png;base64,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" alt="" width="25px" height="25px" />
            </div>
            <img src="@/assets/notification.svg" height="23px" width="23px" />
        </div>
    </div>
</div>
</template>

<script>
import Vue from "vue";
export default {
    name: "NavBar",
    data() {
        return {
            userName: "",
            userId: "",
            profileImage: "",
        };
    },

    created() {
        const userid = JSON.parse(localStorage.getItem("userId"));
        this.axios
            .get(`http://localhost:8082/user/getuser/${userid}`)
            .then((resp) => {
                (this.userId = resp.data.uid),
                (this.userName = resp.data.firstName),
                (this.profileImage = resp.data.profilePicture);
            });
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
        profile() {
            this.$router.push("/IndividualProfile");
        },
        getUserName() {
            const userid = JSON.parse(localStorage.getItem("userId"));
            Vue.axios
                .get(`http://localhost:8082/user/userName/${userid}`)
                .then((resp) => {
                    this.userName = resp.data;
                });
        },
        exit() {
            localStorage.removeItem("userId");
            this.$router.push("/");
        },
        addPost() {
            this.$router.push("/AddPost");
        },
        getData(searchedData) {
            this.$router.push(`SearchBar/${searchedData}`);
            console.log(searchedData);
        },
        adds() {
            this.$router.push("/AddsComponent");
        },
    },
};
</script>

<style scoped>
.search_bar {
    text-align: center;
}

.header {
    display: flex;
    flex-wrap: wrap;
    /* margin-top: 10px; */
    /* justify-content: space-evenly; */
    gap: 80px;
    background-color: white;
    padding: 10px;
    transition: 1s;
    position: fixed;
    width: 100%;
}

#s {
    position: absolute;
    left: 320px;
    top: 20px;
}

.search_btn {
    border: none;
    /* border-radius: 10px; */
}

.logout {
    font-family: bold;
    cursor: pointer;
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
    justify-content: space-evenly;
    width: 40%;
}

.login {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
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
    cursor: pointer;
    border-radius: 50%;
    height: 30px;
    width: 30px;
}

.picture1 {
    border-radius: 50%;
    height: 40px;
    width: 40px;
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
    /* background-color: blue;
     */
    background-color: white;

    /* border-radius: 0px;

    align-items: center;

    padding: 0 30px; */

    border-bottom: none;

    border-bottom: 4px solid #2e81f4;
}

/* .header .login input:hover {
    width: 50px;
    height: 50px;
} */

/* .header .elements input:hover {
    width: 50px;
    height: 50px;
} */

a {
    text-decoration: none;
    color: black;
}

@media only screen and (max-device-width: 480px) {
    .header {
        display: flex;
        flex-wrap: nowrap;
        width: 1080px;
    }

    .login {
        margin-left: -50px;
    }

    a img {
        margin-top: 10px;
    }

    .header .logo input {
        margin-left: -10px;
        width: 150px;

    }

    ::placeholder {
        margin-left: -20px;
        text-align: left;
    }

}

@media only screen and (min-device-width: 480px) and (max-device-width: 800px) {
    .header {
        display: flex;
        flex-wrap: nowrap;
        width: 1080px;
    }

    .login {
        margin-left: -25px;
    }

    a img {
        margin-top: 10px;
    }

    .header .logo input {
        margin-left: -10px;
        width: 150px;
    }

    ::placeholder {
        margin-left: -20px;
        text-align: left;
    }
}
</style>
