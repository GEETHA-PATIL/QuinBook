<template>
<div class="main">
    <div class="header">
        <div class="logo">
            <img src="@/assets/image2.png" alt="facebooklogo" height="40px" width="40px">
        </div>
        <div class="elements">
            <img src="@/assets/home.svg" alt="home" @click.prevent="home">
            <img src="@/assets/watch.svg" alt="watch">
            <img src="@/assets/group.svg" alt="addFriend" @click.prevent="addfriend">
            <a href="https://supermario-game.com/"><img src="@/assets/game.svg" alt="game"></a>
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
    </div>
    
    <div class="Body">
        <div class="left">
            <LeftNavBar />
        </div>
        <div class="middle">
            <div :style="{
                
                  width: '100px',
                  height: '1500px',
                }">
                <br /><br />
                <div class="list" v-for="user in guser" :key="user">

                    <ul class="list">
                        <li class="list-item">
                            <div>
                                <img :src="user.profilePicture" alt="" class="list-item-image" />
                            </div>

                            <div class="list-item-content">
                                <h4>{{user.firstName}}</h4>
                                <p>{{user.lastName}}</p>
                            </div>
                            <!-- <div class="list-item-btn"></div> -->

                            <div class="add-btn" @click="toggle(user.uid,user.email)">
                                <div class="plus">
                                    <img src="https://www.clipartmax.com/png/middle/409-4099027_invite-a-friend-or-family-members-find-a-fitness-partner-invite-a.png" alt="" width="40px" height="35px" />
                                </div>
                                <div class="text">
                                    <div class="button">Add Friend</div>
                                </div>
                            </div>
                        </li>
                    </ul>

                </div>

            </div>
        </div>

    </div>
    <hr>
    <div>
        <p id="ok"><i>&copy;Facebook <strong>2022</strong></i></p>
    </div>
</div>
</template>

<script>
import Vue from "vue"
import LeftNavBar from './LeftNavBar.vue'
export default {
    name: 'SearchBar',
    data() {
        return {
            friends: [],
            guser:[],
            name:'',
        }
    },
    components: {
        LeftNavBar
    },

    created() {
        this.name = this.$route.params.key;
         const userid = JSON.parse(localStorage.getItem('userId'))
            Vue.axios.get(`http://localhost:8082/user/getUsers/${userid}`).then(resp => {
                this.friends = resp.data

            this.guser = this.friends.filter(post =>

                    post.firstName.toLowerCase().includes(this.name.toLowerCase())

                );

            })
        // this.axios.get(`http://localhost:8082/product/getallproduct`).then(resp => {

        //         this.products = resp.data.data

        //         // console.log(resp)

        //         this.products1 = this.products.filter(post =>

        //             post.productName.toLowerCase().includes(this.name.toLowerCase())

        //         );

        //     }

        // )

    },

}
</script>

<style scoped>
.list {
    width: 600px;
    margin-left: -40px;
}

.list-item {
    background: white;
    height: 80px;
    display: flex;
    justify-content: space-between;
    padding-bottom: 5px;
    padding-top: 5px;
    text-decoration: line-b;
    padding-right: 10px;
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.list:last-child {
    border-bottom: none;
}

.list-item-image {
    margin-left: 10px;
    border-radius: 50%;
    width: 70px;
    height:70px;
}

.list-item-content {
    margin-left: -170px;
}

/* .list-item-content{ */

h4,
p {
    margin: 0;
}

h4 {
    margin-top: 10px;
    font-size: 18px;
}

p {
    margin-top: 5px;
    /* color: white-two; */
}

.add-btn {
    display: flex;
    /* justify-content: flex-end; */

    /* flex-direction: row; */
    background-color: rgb(227, 233, 233);
    margin-top: 10px;
    /* margin-left: 200px; */
    /* margin-right: -100px; */
    width: 180px;
    height: 50px;
    /* border: 1px solid #070707; */
    border-radius: 6px;
    cursor: pointer;
    border: 1px solid rgb(151, 148, 148);
    /* box-shadow: 2px 2px 5px 1px rgb(152, 201, 201) ; */
}

.add-btn:hover {
    background-color: rgba(107, 214, 247, 0.637);

    box-shadow: 2px 2px 5px 1px rgb(152, 201, 201);

}

.plus {
    margin-top: 8px;
    margin-left: 10px;
    margin-right: 1px;
}

.text {
    font-size: 20px;

    margin-top: 10px;
    width: 200px;
    height: 20px;
}

.add-image {
    /* margin-top: 5px; */
    margin-right: 5px;
}

.button {
    /* background-color: rgb(255, 255, 255);  */
    border: 0px;
    font-weight: bold;
    font-size: 15px;
    margin-top: 5px;
    margin-top: 5px;

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

/* .logo form {
    margin-top: 10px;
} */

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
    background-image: linear-gradient(to top, rgba(243, 239, 239, 0), rgb(206, 233, 247));
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
    margin-top: 35px;
    margin-left: 15px;
    align-items: center;
    display: flex;
    gap: 10px;
}

.elementstyling {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-left: 10px;
}

.middle {
    display: flex;
    flex-wrap: wrap;
    flex-flow: column;
    flex-direction: column;
    justify-content: left;
    gap: 5%;
    margin: 0 0 0 500px;
    scroll-behavior: smooth;
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

/* .profiles {
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
} */
/* 
.post {
    display: flex;
    flex-wrap: column wrap;
    flex-direction: column;
    justify-content: left;
    background-color: white;
    border: 1px solid white;
    border-radius: 5px;
    margin-top: 20px;
} */

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
    /* gap: 10px; */
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
    gap: 35px;
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
</style>
