<template>
<div>
    <form class="signup-form" action="/register" method="post">
        <div class="form-header">
            <h1>Create Business Account</h1>
        </div>

        <div class="form-body">
            <div class="horizontal-group">
                <div class="form-group left">
                    <label for="firstname" class="label-title">First name *</label>
                    <input type="text" id="firstname" class="form-input" placeholder="Enter your first name" required="required" v-model="firstName" />
                </div>
                <div class="form-group right">
                    <label for="lastname" class="label-title">Last name *</label>
                    <input type="text" id="lastname" class="form-input" placeholder="Enter your last name" required="required" v-model="lastName" />
                </div>
            </div>

            <div class="form-group">
                <label for="email" class="label-title">Email *</label>
                <input type="email" id="email" class="form-input" placeholder="Enter your email" required="required" v-model="emailId" />
            </div>

            <div class="form-group">
                <label for="phone" class="label-title">Phone Number *</label>
                <input type="number" id="phone" class="form-input" placeholder="Enter your Phone number" v-model="phoneNumber" required="required" />
            </div>

            <div class="horizontal-group">
                <div class="form-group left">
                    <label class="label-title"> Gender : </label>
                    <select name="gender" id="" v-model="gender">
                        <option disabled value=""> Please select one</option>
                        <option for="male" name="gender" value="male" id="male">
                            Male
                        </option>
                        <option for="female" name="gender" value="female" id="female">
                            Female
                        </option>
                    </select>
                </div>

                <div class="form-group right">
                    <label for="date" class="label-title"> Date of Birth *</label>
                    <input type="date" id="date" class="form-input" placeholder="dd/mm/yyyy" v-model="DOB" required="required" />
                </div>
            </div>

            <div class="horizontal-group">
                <div class="form-group left">
                    <label for="password" class="label-title">Password *</label>
                    <input type="password" id="password" class="form-input" placeholder="Enter your password" v-model="password1" required="required" />
                </div>

                <div class="form-group right">
                    <label for="confirm-password" class="label-title">Confirm Password *</label>
                    <input type="password" class="form-input" id="confirm-password" placeholder="Enter your password again" v-model="password2" required="required" />
                </div>
            </div>

            <div class="horizontal-group">
                <div class="form-group">
                    <label for="choose-file" class="label-title">Upload Profile Picture :
                    </label>
                    <input type="file" id="choose-file" size="80" @click="processFile($event)" />
                </div>
            </div>

            <div class="form-group right">
                <label class="label-title">Categories : </label>
                <hr />
                <div class="interests">

                    <input type="radio" name="fav_language" value="Shopping" v-model="interest" />Shopping
                    <input type="radio" name="fav_language" value="Anime" v-model="interest" />Anime
                    <input type="radio" name="fav_language" value="Electronics" v-model="interest" />Electronics
                    <input type="radio" name="fav_language" value="Movies" v-model="interest" />Movies
                    <input type="radio" name="fav_language" value="Watches" v-model="interest" /> Watches
                </div>
            </div>
        </div>

        <div class="form-footer">
            <button type="submit" @click.prevent="postData" method="post" class="btn">Sign Up</button><br />
            <label for=""> Already have an Account?</label>
        </div>
    </form>
</div>
</template>

<script>
export default {
    name: "BusinessSignup",
    data() {
        return {
            firstName: '',
            lastName: '',
            emailId: '',
            DOB: '',
            phoneNumber: '',
            gender: '',
            password1: '',
            password2: '',
            images: '',
            interest: ''
        }
    },
    methods: {
        processFile(event) {
            this.someData = event.target.files[0]
        },
        postData() {

            this.axios.post(`http://localhost:8083/addBusinessUser`, {
                    firstName: this.firstName,
                    lastName: this.lastName,
                    email: this.emailId,
                    dateOfBirth: this.DOB,
                    phno: this.phoneNumber,
                    security: this.security,
                    gender: this.gender,
                    password: this.password1,
                    profilePicture: this.images,
                    category: this.interest

                })
                .then((result) => {
                    this.$router.push('/BusinessLogin')
                    console.log("Result", result)
                })

        }
    }

};
</script>

<style scoped>
/* .full {
  margin-left: 300px;
  width: 700px;
  margin-right: 300px;
  width: 100%;
  -webkit-filter: grayscale(50%);
  filter: grayscale(40%);
  opacity: 0.2;
  animation-name: animar_fondo;
  animation-duration: 20s;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  animation-direction: alternate;
  background: url("https://images.unsplash.com/42/U7Fc1sy5SCUDIu4tlJY3_NY_by_PhilippHenzler_philmotion.de.jpg?ixlib=rb-0.3.5&q=50&fm=jpg&crop=entropy&s=7686972873678f32efaf2cd79671673d");
}

@-webkit-keyframes animar_fondo {
  from {
    -webkit-transform: scale(1) translate(0px);
    -moz-transform: scale(1) translate(0px);
    -ms-transform: scale(1) translate(0px);
    -o-transform: scale(1) translate(0px);
    transform: scale(1) translate(0px);
  }
  to {
    -webkit-transform: scale(1.5) translate(50px);
    -moz-transform: scale(1.5) translate(50px);
    -ms-transform: scale(1.5) translate(50px);
    -o-transform: scale(1.5) translate(50px);
    transform: scale(1.5) translate(50px);
  }
}

.cont_back_info {
  position: relative;
  float: left;
  width: 640px;
  height: 980px;
  overflow: hidden;
  background-color: #fff;
  margin-top: 100px;
  box-shadow: 1px 10px 30px -10px rgba(0, 0, 0, 0.5);
  z-index: 2;
}

.cont_img_back_grey {
  position: absolute;
  width: 950px;
  height: 1000px;
  top:-80px;
}

.cont_img_back_grey > img {
  width: 100%;
  -webkit-filter: grayscale(100%);
  filter: grayscale(100%);
  opacity: 0.2;
  animation-name: animar_fondo;
  animation-duration: 20s;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  animation-direction: alternate;
  z-index: -2;
} */

.signup-form {
    font-family: sans-serif;
    width: 600px;
    margin: 30px auto;
    /* background: linear-gradient(to right, #ffffff 0%, #fafafa 50%, #ffffff 99%); */
    border-radius: 10px;
    /* background: url("https://images.unsplash.com/42/U7Fc1sy5SCUDIu4tlJY3_NY_by_PhilippHenzler_philmotion.de.jpg?ixlib=rb-0.3.5&q=50&fm=jpg&crop=entropy&s=7686972873678f32efaf2cd79671673d"); */
    /* width: 100%; */
    /* -webkit-filter: grayscale(100%);     filter: grayscale(100%); */
    /* opacity: 0.2; */
    /* animation-name: animar_fondo;
  animation-duration: 20s;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  animation-direction: alternate;
  z-index: -2; */
}

.form-header {
    background-color: rgb(48, 155, 197);
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}

.form-header h1 {
    font-size: 30px;
    text-align: center;
    color: white;
    padding: 20px 0;
    border-bottom: 1px solid #cccccc;
}

.form-body {
    padding: 10px 40px;
    text-align: left;
}

.form-group {
    margin-bottom: 20px;
}

.form-body .label-title {
    color: #1bb5ba;
    font-size: 17px;
    text-align: left;
}

.form-body .form-input {
    font-size: 17px;
    box-sizing: border-box;
    width: 100%;
    height: 34px;
    padding-left: 10px;
    padding-right: 10px;
    color: #333333;
    text-align: left;
    border: 1px solid #d6d6d6;
    border-radius: 4px;
    background: white;
    outline: none;
}

.horizontal-group .left {
    float: left;
    width: 49%;
}

.horizontal-group .right {
    float: right;
    width: 49%;
}

.signup-form {
    box-shadow: 0 2px 4px rgb(0 0 0 / 10%), 0 8px 16px rgb(0 0 0 / 10%);
    box-sizing: border-box;
}

input[type="file"] {
    outline: none;
    cursor: pointer;
    font-size: 17px;
}

::-webkit-input-placeholder {
    color: #d9d9d9;
}

.form-footer {
    clear: both;
}

.signup-form .form-footer {
    background-color: #eff0f1;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
    padding: 10px 40px;
    text-align: center;
    border-top: 1px solid #cccccc;
}

select {
    size: 400px;
    height: 34px;
    width: 100%;
    border-radius: 4px;
    text-align: center;
    font-size: 17px;
    border: 1px solid #d6d6d6;
}

.interests {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}

#choose-file {
    border: none;
}

.btn {
    display: inline-block;
    padding: 10px 20px;
    background-color: #1ba2ba;
    font-size: 17px;
    border: none;
    border-radius: 5px;
    color: #bcf5e7;
    cursor: pointer;
}

.btn:hover {
    background-color: #169c7b;
    color: white;
}
</style>
