<template>
    <MDBRow class="flex-nowrap d-flex">
        <MDBCol class="w-100 d-flex flex-column flex-nowrap justify-content-between mx-auto" style="max-width: 440px;">
            <MDBRow class="flex-nowrap d-flex align-items-center">
                <MDBCol class="w-100">
                    <img class="float-start" src="src/assets/imgs/logo_login.svg" alt="" width="200">
                </MDBCol>
                <MDBCol class="flex-shrink-1" col="auto">
                    <img src="src\assets\imgs\繁體中文.svg" alt="">
                </MDBCol>
            </MDBRow>
            <div class="py-5" v-if="chooseRole">
                <div class="mb-5">
                    <div class="text-start fw-bold h2">歡迎回來!</div>
                    <div class="text-start">
                        請選擇您的身份進行登入，或者
                        <span class="text-primary" sytle="cursor: pointer">立即註冊</span>
                    </div>
                </div>
                <div class="py-3 rounded bg-white user">
                    <div class="row row-gap-2 items-end flex-nowrap" @click="manageRole">
                        <MDBRow class="flex-nowrap d-flex align-items-center flex-wrap">
                            <MDBCol class="w-100 d-flex flex-column align-items-start">
                                <p>我是房東/管理者</p>
                                <span class="text-primary">前往登入<img src="src/assets/imgs/navigate_next.svg" alt=""></span>
                            </MDBCol>
                            <MDBCol class="flex-shrink-1" style="margin-top: -122px;" col="auto">
                                <img src="src/assets/imgs/管理者.svg" alt="">
                            </MDBCol>
                        </MDBRow>
                    </div>
                </div>
                <div class="py-3 rounded bg-white user">
                    <div class="row row-gap-2 items-end flex-nowrap" @click="tenantRole">
                        <MDBRow class="flex-nowrap d-flex align-items-center flex-wrap">
                            <MDBCol class="w-100 d-flex flex-column align-items-start">
                                <p>我是租客</p>
                                <span class="text-primary">前往登入<img src="src/assets/imgs/navigate_next.svg" alt=""></span>
                            </MDBCol>
                            <MDBCol class="flex-shrink-1" style="margin-top: -122px;" col="auto">
                                <img src="src/assets/imgs/我是租客.svg" alt="">
                            </MDBCol>
                        </MDBRow>
                    </div>
                </div>
            </div>
            <div class="py-5" v-if="roleDiv">
                <div class="md-5">
                    <div class="text-start fw-bold h2">歡迎 <label class="start-label">{{ role }}</label></div>
                    <div class="text-start mb-3">
                        還沒有帳號嗎？
                        <span class="text-primary" sytle="cursor: pointer">立即註冊</span>
                    </div>
                </div>
                <div>
                    <div class="d-flex justify-content-between input-width">
                        <label for="">帳號</label>
                        <div class="btn-toolbar justify-content-end " role="toolbar"
                            aria-label="Toolbar with button groups">
                            <MDBBtnGroup class="me-2 text-nowrap shadow-none" aria-label="First group">
                                <MDBBtn :class="[activeTab === 'email' ? 'active-btn' : 'unactive-btn']"
                                    @click="activeTab = 'email'">E-mail
                                </MDBBtn>
                            </MDBBtnGroup>
                            <MDBBtnGroup class="me-2 text-nowrap shadow-none" aria-label="Second group">
                                <MDBBtn :class="[activeTab === 'phone' ? 'active-btn' : 'unactive-btn']"
                                    @click="activeTab = 'phone'">手機號碼
                                </MDBBtn>
                            </MDBBtnGroup>
                        </div>
                    </div>
                    <div class="mb-4">
                        <input v-if="activeTab === 'email'" class="loginInput" placeholder="請輸入E-mail" type="email" />
                        <div v-else-if="activeTab === 'phone'" class=" input-width">
                            <div class="d-flex mb-1">
                                <select :disabled="isDisabled" name="" id="" class="phoneSelect">
                                    <option value="🇹🇼 (886)">🇹🇼 (886)</option>
                                </select>
                                <input class="phoneInput" placeholder="0912345678" type="text" />
                            </div>
                            <div class="info">
                                <p>
                                    <img src="src/assets/imgs/icons/information.svg" alt="">號碼最長為 10 碼。
                                </p>
                            </div>
                        </div>
                    </div>
                    <div class="d-flex justify-content-between input-width">
                        <label for="">密碼</label>
                        <div class="mb-2 justify-content-end">
                            <img :src="state.isActive ? 'src/assets/imgs/icons/eye.svg' : 'src/assets/imgs/icons/eye_off.svg'"
                                alt="" @click="toggleImage" />
                        </div>
                    </div>
                    <div class="mb-4 ">
                        <input :type="state.passwordVisible ? 'text' : 'password'" class="loginInput" placeholder="請輸入密碼" />
                    </div>
                    <div class="mb-4">
                        <MDBCheckbox label="記住我" v-model="checkbox1" />
                    </div>
                    <div class="d-grid gap-2 mb-5">
                        <MDBBtn color="primary" class="login-btn disabled">立即登入</MDBBtn>
                    </div>
                    <div class="tableTitle mb-5">
                        <span class="midText">或者</span>
                    </div>
                    <div class="d-flex justify-content-center input-width mb-5">
                        <img class="iconImg" src="src/assets/imgs/fullfacebook.svg" alt="">
                        <img class="iconImg" src="src/assets/imgs/Google.svg" alt="">
                        <img class="iconImg" src="src/assets/imgs/fullline.svg" alt="">
                    </div>
                    <!-- Flexbox for demo purpose -->
                    <div class="d-flex justify-content-center input-width dividers">
                        <!-- Element on the left -->
                        <div class="px-4" @click="forgotPassword">
                            <p>忘記密碼?</p>
                        </div>
                        <!-- Vertical divider -->
                        <div class="vr" style="height: 28px; background-color: #e2e2e2; --mdb-divider-width:1px"></div>
                        <!-- Element on the left -->
                        <div class="px-4">
                            <p>忘記帳號?</p>
                        </div>
                    </div>
                </div>
            </div>
            <div v-if="passwordDiv">
                <div class="py-5" v-if="!oldDiv">
                    <div class="md-5">
                        <div class="text-start fw-bold h2" style="font-size: 36px;">忘記密碼嗎？</div>
                        <div class="text-start mb-3" style="font-size: 16px; color: #a3a3a3; width: 441px;">
                            在重新設定密碼前，請先完成帳號驗證，即可進行重設密碼。
                        </div>
                    </div>
                    <div>
                        <div class="d-flex justify-content-between input-width">
                            <label for="">帳號</label>
                            <div class="btn-toolbar justify-content-end " role="toolbar"
                                aria-label="Toolbar with button groups">
                                <MDBBtnGroup class="me-2 text-nowrap shadow-none" aria-label="First group">
                                    <MDBBtn :class="[activeTab === 'email' ? 'active-btn' : 'unactive-btn']"
                                        @click="activeTab = 'email'">E-mail
                                    </MDBBtn>
                                </MDBBtnGroup>
                                <MDBBtnGroup class="me-2 text-nowrap shadow-none" aria-label="Second group">
                                    <MDBBtn :class="[activeTab === 'phone' ? 'active-btn' : 'unactive-btn']"
                                        @click="activeTab = 'phone'">手機號碼
                                    </MDBBtn>
                                </MDBBtnGroup>
                            </div>
                        </div>
                        <div class="mb-4">
                            <input v-if="activeTab === 'email'" v-model="emailInput" class="loginInput"
                                placeholder="請輸入E-mail" type="email" />
                            <div v-else-if="activeTab === 'phone'" class=" input-width">
                                <div class="d-flex mb-1">
                                    <select :disabled="isDisabled" name="" id="" class="phoneSelect">
                                        <option value="🇹🇼 (886)">🇹🇼 (886)</option>
                                    </select>
                                    <input class="phoneInput" v-model="phoneNumber" placeholder="0912345678" type="text" />
                                </div>
                                <div class="info">
                                    <p>
                                        <img src="src/assets/imgs/icons/information.svg" alt="">號碼最長為 10 碼。
                                    </p>
                                </div>
                            </div>
                        </div>
                        <div class="d-grid gap-2 mb-4">
                            <MDBBtn color="primary" class="login-btn" :disabled="isButtonDisabled" @click="toggleDivs">驗證帳號
                            </MDBBtn>
                        </div>
                        <div>
                            <MDBBtn class="return-btn disabled">返回登入</MDBBtn>
                        </div>
                    </div>
                </div>
                <div v-if="showDiv">
                    <Verification />
                </div>
                <div v-if="showPhoneDiv">
                    <VerificationPhone />
                </div>
            </div>
            <div class="text-center power-by">
                <img src="src/assets/imgs/powered_by.svg" alt="">
            </div>
        </MDBCol>
        <MDBCol class="d-none d-lg-block flex-shrink-1" col="auto">
            <img src="src/assets/imgs/login_right_photo.png" alt="" class="float-end">
        </MDBCol>
    </MDBRow>
    <Footer />
</template>

<script setup lang="ts">
import { MDBCol, MDBRow, MDBBtnGroup, MDBBtn, MDBCheckbox } from "mdb-vue-ui-kit"
import Footer from "../layout/Footer.vue"
import { ref, reactive } from "vue"
import Verification from "../password/VerificationCodeEmail.vue"
import VerificationPhone from "../password/VerificationCodePhone.vue"

const chooseRole = ref(true)
const role = ref('')
const roleDiv = ref(false)
const passwordDiv = ref(false)

const manageRole = () => {
    role.value = '房東/管理者！';
    chooseRole.value = false; // 隐藏 chooseRole
    roleDiv.value = true;
};
const tenantRole = () => {
    role.value = '租客！';
    chooseRole.value = false; // 隐藏 chooseRole
    roleDiv.value = true;
};

const forgotPassword = () => {
    roleDiv.value = false; 
    passwordDiv.value = true;
}

const checkbox1 = ref(false);
const activeTab = ref('email'); // 默認選中
const isDisabled = ref(true);
const phoneNumber = ref('');
const emailInput = ref('');
const state = reactive({
    isActive: false,
    passwordVisible: false
});
const toggleImage = () => {
    state.isActive = !state.isActive;
    state.passwordVisible = !state.passwordVisible;
};
const isButtonDisabled = false;
// computed(() => {
//     if (emailInput.value === '' || phoneNumber.value.length !== 10) {
//         return true;
//     }
// });

const oldDiv = ref(false);
const showDiv = ref(false);
const showPhoneDiv = ref(false);

function toggleDivs() {
    if(activeTab.value === 'email'){
        oldDiv.value = !oldDiv.value;
        showDiv.value = !showDiv.value;
    }else if(activeTab.value === 'phone'){
        oldDiv.value = !oldDiv.value;
        showPhoneDiv.value = !showPhoneDiv.value;
    }
}


</script>

<style scoped lang="scss">
::v-deep .form-check-input[type=checkbox] {
    border-color: #464444;
    border-radius: 0.15rem;
}

.user {
    padding-left: 1.5rem !important;
    padding-right: 0.5rem !important;
    cursor: pointer;
    height: 143px;
    width: 440px;
    transition: all 0.1s ease 0s;
    box-shadow: rgba(68, 68, 68, 0.3) 0px 2px 8px 0px;
    margin-top: 120px;
}

.power-by {
    padding-bottom: 100px;
}
</style>
