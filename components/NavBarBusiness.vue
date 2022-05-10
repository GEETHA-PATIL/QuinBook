<template>
<div class="Header1">
    <div class="header2">
        <span class="image"><img src="@/assets/image2.png" alt="logo" height="70px" width="70px"></span>
        <span class="quin">
            <marquee><h2>QuinBook</h2></marquee>
        </span>

        <!-- <img class="logo" src="https://media-exp1.licdn.com/dms/image/C560BAQFKqMssV3K9Zg/company-logo_200_200/0/1624347145031?e=2147483647&v=beta&t=1sXUoK6HA4YiGC9KjLUBn9nr9xmXrp3ohffR72AH4Es" alt=""> -->
        <!-- <button class="button">Sign Up</button> -->
    </div>
    <div class="class1">
        <span>
            <h2>Create a Page</h2>
        </span>
        <span>
            <p>Connect your business, yourself or your cause to the worldwide community of people on Quinbook. To get started, choose a Page category.</p>
        </span>
    </div>
    <div class="class2">
        <div class="content">
            <span><img class="src" src="https://assets.materialup.com/uploads/01d7570f-01ca-4e3a-8dc1-b8a16864f916/preview.jpg" alt=""></span>
            <span><b> Business and Brand</b></span>
            <span>Showcase your products and services, spotlight your brand and reach more customers on Quinbook.</span>
        </div>
        <router-link :to="{name:'BusinessLogin'}">
            <button class="G" type="submit">Get started</button>
        </router-link>
        <!-- <hr> -->
        <router-link :to="{name:'BusinessSignup'}">
            <button class="sign" type="submit"> Sign Up</button>
        </router-link>
    </div>
    <!-- <div class="footer">
        <h4>vishnu</h4>
    </div> -->
</div>
</template>

<script>
export default {
    name: 'NavBarBusiness'
}
</script>

<style scoped>
.Header1 {
    /* background-color: rgb(195, 223, 209); */
    background-color: white;
    /* height: 100vh; */
}
.image{
    margin-top: 6px;
}
.header2 {
    display: flex;
    background-color: rgb(69, 135, 209);
    height: 70px;
    align-items: center;
    gap:10px;
    /* position: fixed; */
}

/* .button{
        margin-left: 300px;
        background-color: rgb(47, 255, 109);
        height: 30px;
} */
.class2 {
    background-color: white;
    margin-left: 100px;
    margin-right: 100px;
    margin-bottom: 7px;
    margin-top: 33px;
    border-radius: 17px;
    border: 1px solid black
}

.class1 {
    display: flex;
    flex-direction: column;
    align-items: center;
    cursor: pointer;
}

/* .class1:hover {
    background-color: rgba(209, 201, 201, 0.904);
} */

.img1 {
    margin-left: 168px;
}

.b {
    margin-left: 137px;
    margin-top: 37px;
    font-size: 30px;
}

.S {
    margin-left: 109px;
    margin-right: 56px;
    font-size: 15px;
    margin-top: 52px;
}

.G {
    margin-top: 71px;
    /* margin-left: 231px; */
    border: none;
    width: 268px;
    margin-bottom: 52px;
    height: 42px;
    background-color: aliceblue;
    border-radius: 8px;
    margin-left: 35px;
    cursor: pointer;

}

.content {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.G:hover {
    background-color: mediumspringgreen;
    border: 1px solid black;

}

.src {
    margin-top: 15px;
    height: 205px;
}

.logo {
    height: 10px;
}

.quin {

    /* margin-top: 49px; */
    font-size: 30px;
    color: aliceblue;

}

.sign {
    margin-bottom: 15px;
    /* margin-left: 236px; */
    width: 271px;
    height: 42px;
    /* width: 77px; */
    border: none;
    border-radius: 10px;
    background-color: aliceblue;
    cursor: pointer;
}

.sign:hover {
    background-color: mediumspringgreen;
    border: 1px solid black;
}
</style>
