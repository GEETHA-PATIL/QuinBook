<template>
<div class="user">
    <div class="content-title">
        <div class="content">
            <img src="@/assets/image2.png" alt="logo" height="200px" width="200px">
            <h1 class="title">QuinBook</h1>
        </div>
        <div class="slogan">
            <h3>The only book that you can use without getting bored</h3>
        </div>
    </div>
    <div class="create">
        <div class="user-login">
            <div v-if="errors.length">
                <h5 v-for="error in errors" :key="error">{{error}}</h5>
            </div>

            <form class="login">
                <input type="text" v-model="posts.email" placeholder="Enter your E-mail" />
                <input type="password" v-model="posts.password" placeholder="Enter Password" />
                <button class="submitbutton" @click.prevent="postData" type="submit" method="post"><b>
                        <h2>Log In</h2>
                    </b></button>
            </form>
            <div class="forget">
                <router-link :to="{name:'ForgetPassword'}"> Forgotten Password?</router-link>
            </div>
            <div>
                <hr>
            </div>
            <button class="create-Account" @click="register">Create New Account</button>
        </div>
        <router-link :to="{name: 'NavBarBusiness'}">
            <p><u><b>Create a page</b></u> for bussiness</p>
        </router-link>
    </div>

    <!-- <router-link to="/UserHome" > Forgotten Password?</router-link> -->
</div>
</template>

<script>
// import qs from "qs";
import axios from "axios";
import Vue from 'vue';
import VueAxios from 'vue-axios';
import swal from 'sweetalert'

Vue.use(VueAxios, axios)
export default {
    name: "UserLogin",
    data() {
        return {
            posts: {
                email: '',
                password: '',
            },
            errors: []
        }
    },
    methods: {
        postData() {
            // this.axios.post(`http://10.20.2.203:9093/oauth/token`, qs.stringify({
            //     'grant_type': 'password',
            //     'username': this.posts.email,
            //     'password': this.posts.password
            // }), {
            //     headers: {
            //         'Authorization': 'Basic UXVpbmJvb2s6YWFhYQ==',
            //         'Content-Type': 'application/x-www-form-urlencoded'
            //     }
            // }).then((resp) => {
            //     console.log(resp.data.access_token)
            //     sessionStorage.setItem("Authorization", resp.data.access_token);
            // }).catch((error) => {
            //     console.log("User details doesnot match" + error.response.data.error)
            //     swal({
            //         title: "check crendentials",
            //         text: "and try again",
            //         icon: "error",
            //         button: "OKAY",

            //     })

            // })

            this.errors = [];
            if (!this.posts.email) {
                this.errors.push("Please enter your email")
            } else if (!this.posts.password) {
                this.errors.push("Please enter your password")
            }

            if (this.errors.length == 0) {
                this.axios.get(`http://localhost:8082/user/validation/${this.posts.email}/${this.posts.password}`, this.posts)
                    .then((Response) => {
                        console.log("Response", Response.data)
                        // console.log("Result", Response.data.result)
                        if (Response.data.result) {
                            console.log("Error", Response.data.result)

                            localStorage.setItem('userId', JSON.stringify(Response.data.data))
                            localStorage.setItem('userEmail', JSON.stringify(this.posts.email))

                            this.$router.push('/UserHome')
                        } else {
                            swal({
                                title: "check crendentials",
                                text: "and try again",
                                icon: "error",
                                button: "OKAY",

                            })
                            // this.$router.push('/')
                            this.alert("Please check your Credentials")
                        }
                    })

            }
        },
        register() {
            this.$router.push("/UserSignup")
        }

    }
}
</script>

<style scoped>
.user {
    display: flex;
    flex-wrap: wrap;
    gap: 10%;
    background-color: #f0f2f5;
    height: 100VH;

}

.create {
    margin-top: 5%;
}

.content-title {
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    margin-left: 12%;
    margin-top: 10%;

}

.user-login {
    box-shadow: 0 2px 4px rgb(0 0 0 / 10%), 0 8px 16px rgb(0 0 0 / 10%);
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    height: 400px;
    width: 396px;
    padding: 20px;
    background-color: white;
    margin-top: 10%;
    border-radius: 10px;
    margin-bottom: 10px;
    gap: 10px;

}

.login {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

@media only screen and (max-device-width: 350px) {
    .user {
        display: flex;
        flex-wrap: nowrap;
        flex-direction: column;
        margin-top: -20px;
        width: 650px;
        height: 100%;
    }

    .content {
        width: 550px;
    }

    .content img {
        width: 150px;
        height: 150px;
    }

    .create {
        width: 550px;
        margin-left: 95px;
        margin-top: -40px;
    }

    .user-login {
        height: 350px;
        margin-bottom: 50px;
    }

    p {
        margin-left: -80px;
    }

    .slogan {
        margin-top: -30px;
    }
}

@media only screen and (min-device-width: 350px) and (max-device-width: 850px) {
    .user {
        display: flex;
        flex-wrap: nowrap;
        flex-direction: column;
        margin-top: -20px;
        height: 100%;
        width: 100%;
    }

    .content {
        width: 550px;
    }

    .content img {
        width: 150px;
        height: 150px;
    }

    .create {
        width: 550px;
        margin-left: 140px;
        margin-top: -40px;
    }

    .user-login {
        height: 350px;
        margin-bottom: 50px;
    }

    p {
        margin-left: -100px;
    }
}

input {
    background: #FFFFFF;
    border: 1px solid #dddfe2;
    border-radius: 5px;
    height: 35px;
    padding: 10px;
}

.create-Account {
    width: 150px;
    height: 40px;
    margin-left: 30%;
    background: #42b72a;
    color: white;
}

button {
    height: 50px;
    cursor: pointer;
    background-color: #1877f2;
    border-radius: 7px;
    border: none;
}

.forget {
    color: #1877f2;
    cursor: pointer;
}

.submitbutton {
    color: white;

}

.title {
    font-size: 5em;
    color: #42b72a;
}

.content {
    display: flex;
    align-items: center;
}

p {
    font-size: 20px;
    cursor: pointer;
}
</style>
