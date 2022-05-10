<template>
<div class="main">
    <div class="header">
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
    </div>
    <div class="Body">
        <div class="left">
            <div class="profile">
                <img src="@/assets/myimage.jpeg" class="picture" alt="christod">
                G.V.S.Kumar
            </div>
            <a href="https://www.covid19india.org/"><div class="elementstyling">
                <img src="@/assets/covid.png" alt="covid">
                COVID-19 Information Center
            </div></a>
            <div class="elementstyling">
                <img src="@/assets/page.png" alt="pages">
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
        </div>
        <div class="middle">
        
        </div>
        <div class="right">
            <div class="profile">
                <img src="@/assets/team-2.jpg" alt="team2" class="picture1">
                Sheikh kalim
            </div>
            <div class="elementstyling">
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
        </div>
    </div>
    <hr>
    <div>
        <p id="ok"><i>&copy;Facebook <strong>2022</strong></i></p>
    </div>
</div>
</template>

<script>
export default {
    name: "UserBusinessPage",

    methods:{
        addfriend(){
            this.$router.push("/AddFriends")
        },
        getFriends(){
            this.$router.push("/FriendsLists")
        },
        home(){
            this.$router.push("/UserHome")
        }
    }
}
</script>

<style scoped>
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
    background-image: linear-gradient(to top, rgba(243, 239, 239, 0), rgb(206, 233, 247));
    scroll-behavior: auto;
}

.Body {
    display: flex;
    flex-flow: row wrap;
    flex-direction: row;
    gap: 13%;
    flex-wrap: wrap;
    padding:40px 0 0 0;
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
.profile:hover{
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
    margin-left:1150px;
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
a{
    text-decoration: none;
    color:black;
}
</style>
