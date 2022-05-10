<template>
<div>
    <form class="signup-form" action="/register" method="post">
        <div class="form-header">
            <h1>Create User Account</h1>
        </div>
        
        <div class="form-body">
            <div class="horizontal-group">
                <div v-if="errors.length">
                <h5 v-for="error in errors" :key="error">{{error}}</h5>
            </div>
                <div class="form-group left">
                    <label for="firstname" class="label-title">First name *</label>
                    <input type="text" id="firstname" class="form-input" placeholder="Enter your first name" required="required" v-model="firstName" />
                </div>
                <div class="form-group right">
                    <label for="lastname" class="label-title">Last name *</label>
                    <input type="text" id="lastname" class="form-input" placeholder="Enter your last name" v-model="lastName" />
                </div>
            </div>

            <div class="form-group">
                <label for="email" class="label-title">Email *</label>
                <input type="email" id="email" class="form-input" placeholder="Enter your email" required="required" v-model="emailId" />
            </div>
            <div class="form-group">
                <label for="phone" class="label-title">Phone Number *</label>
                <input type="phone" id="phone" class="form-input" placeholder="Enter your Phone number" required="required" v-model="phoneNumber" />
            </div>

            <!-- <div class="horizontal-group">
                <div class="form-group">
                    <label for="account" class="label-title">Account Type :
                    </label>

                    <input type="radio" id="account" name="account" value="Public" v-model="security" />Public
                    <input type="radio" id="account" name="account" value="Private" v-model="security" />Private
                </div>
            </div> -->

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
                    <input type="date" id="date" class="form-input" placeholder="dd/mm/yyyy" required="required" v-model="DOB" />
                </div>
            </div>

            <div class="horizontal-group">
                <div class="form-group left">
                    <label for="password" class="label-title">Password *</label>
                    <input type="password" id="password" class="form-input" placeholder="Enter your password" required="required" v-model="password1" />
                </div>

                <div class="form-group right">
                    <label for="confirm-password" class="label-title">Confirm Password *</label>
                    <input type="password" class="form-input" id="confirm-password" placeholder="Enter your password again" required="required" v-model="password2" />
                </div>
            </div>

            <div class="horizontal-group">
                <div class="form-group">
                    <label for="choose-file" class="label-title">Upload Profile Picture :
                    </label>
                    <!-- <input type="file"  v-model="fileInput" id="choose-file" size="80"   /> -->
                    <!-- @click="processFile(event)" -->
                    <input type=text v-model="images" id="choose-file" size="80" />

                </div>
            </div>

            <div class="form-group right">
                <label class="label-title">Interests : </label>
                <hr>
                <div class="interests">
                    <label> <input type="checkbox" value="shopping" v-model="interest" />Shopping</label>
                    <label> <input type="checkbox" value="technology" v-model="interest" />Technology</label>
                    <label> <input type="checkbox" value="learning" v-model="interest" />Learning</label>
                    <label> <input type="checkbox" value="food" v-model="interest" />Food</label>
                    <label> <input type="checkbox" value="entertainment" v-model="interest" /> Entertainment</label>
                </div>
            </div>
        </div>

        <div class="form-footer">
            <button type="submit" @click.prevent="postData" method="post" class="btn">Sign Up</button><br>
            <u>
                <label for="" @click.prevent="login"> Already have an Account?</label>
            </u>
        </div>
    </form>
</div>
</template>

<script>
export default {
    name: "UserSignup",
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
            security: '',
            interest: [],
            errors:[]

        }
    },
    methods: {
        processFile(event) {
            this.someData = event.target.files[0]
        },
        handleFileUpload(event) {
            this.file = event.target.files;
        },

        postData() {
            this.errors = [];
            if (!this.emailId) {
                this.errors.push("Please enter your email")
            } else if (!this.password1) {
                this.errors.push("Please enter your password")
            } else if (!this.password2) {
                this.errors.push("Please re-enter your password")
            } else if (!this.firstName) {
                this.errors.push("Please enter your first name")
            } else if (!this.phoneNumber) {
                this.errors.push("Please enter your phone number")
            } else if (!this.DOB) {
                this.errors.push("Please enter your date of birth")
            } else if (!this.gender) {
                this.errors.push("Please enter your gender")
            }

            if (this.errors.length == 0) {
                // this.axios.post('http://10.20.2.203:9093/add', {
                //     userName: this.emailId,
                //     // userName: this.userName,
                //     password: this.password1,
                //     userType: this.security.toLowerCase(),
                //     emailId: this.emailId,

                // })

                this.axios.post(`http://localhost:8082/user/addUser`, {
                        firstName: this.firstName,
                        lastName: this.lastName,
                        email: this.emailId,
                        dateOfBirth: this.DOB,
                        phno: this.phoneNumber,
                        security: 'public',
                        gender: this.gender,
                        password: this.password1,
                        profilePicture: this.images,
                        interests: this.interest

                    })
                    .then((result) => {
                        this.$router.push('/')
                        console.log("Result", result)
                    })

                this.axios.post(`http://10.20.2.212:8082/Ads/User`, {
                    userName: this.emailId,
                    interests: this.interest,
                    platform: "quinbook"
                })
            }

        },
        login(){
            this.$router.push("/");
        }

    }

};
</script>

<style scoped>
.signup-form {
    font-family: sans-serif;
    width: 600px;
    margin: 30px auto;
    /* background: linear-gradient(to right, #ffffff 0%, #fafafa 50%, #ffffff 99%); */
    border-radius: 10px;
}

.form-header {
    /* background-color: #eff0f1; */
    background-color: rgb(48, 155, 197);
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}

.form-header h1 {
    font-size: 30px;
    text-align: center;
    /* color: #666; */
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

.signup-form {
    box-shadow: 0 2px 4px rgb(0 0 0 / 10%), 0 8px 16px rgb(0 0 0 / 10%);
    box-sizing: border-box;
}

.signup-form .form-footer {
    background-color: #eff0f1;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
    padding: 10px 40px;
    text-align: center;
    border-top: 1px solid #cccccc;
}
@media only screen and (min-device-width: 150px) and (max-device-width: 300px) {
  .signup-form {
    display: flex;
    flex-direction: column;
    /* align-items: center; */
    width: 550px;
    padding: 100px;
  }
}
@media only screen and (min-device-width: 300px) and (max-device-width: 650px) {
  .signup-form {
    display: flex;
    flex-direction: column;
    width: 850px;
    padding-left: 250px;
  }
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
