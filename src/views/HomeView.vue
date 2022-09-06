<template>
    <div>
        <form @submit.prevent="submit" @reset.prevent="reset" class="mx-5">
            <div class="row">
                <div class="form-group col-md-6 mb-4 px-5">
                    <label for="first-name" class="form-label fw-bold text-uppercase">
                        First name 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="text" 
                        class="form-control" 
                        id="first-name" 
                        autocomplete="given-name"
                        v-model="formData.save.firstName" 
                        @keyup="formatName"
                        @input="resetError('firstName')"
                    >
                    <div v-if="errors.firstName">
                        <small v-for="(err, i) in errors.firstName" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-5">
                    <label for="gender" class="form-label fw-bold text-uppercase">
                        Gender 
                        <span class="text-danger">*</span>
                    </label>
                    <select class="form-select" id="gender" v-model="formData.save.gender" @input="resetError('gender')">
                        <option value="" disabled>Choose gender</option>
                        <option value="Male">Male</option>
                        <option value="Female">Female</option>
                    </select>
                    <div v-if="errors.gender">
                        <small v-for="(err, i) in errors.gender" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-5">
                    <label for="last-name" class="form-label fw-bold text-uppercase">
                        Last name 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="text" 
                        class="form-control" 
                        id="last-name" 
                        autocomplete="family-name"
                        v-model="formData.save.lastName" 
                        @keyup="formatName" 
                        @input="resetError('lastName')"
                    >
                    <div v-if="errors.lastName">
                        <small v-for="(err, i) in errors.lastName" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-5">
                    <label class="form-label fw-bold text-uppercase">
                        Payment mode 
                        <span class="text-danger">*</span>
                    </label>
                    <div class="text-capitalize fw-normal">
                        <div class="form-check-inline d-inline-flex align-items-center lh-lg">
                            <input 
                                class="custom-check-input" 
                                type="radio" 
                                v-model="formData.notSave.paymentMode" 
                                id="inlineRadio1" 
                                value="Visa" 
                                @input="resetError('paymentMode')"
                            >
                            <label class="form-check-label" for="inlineRadio1">Visa</label>
                        </div>
                        <div class="form-check form-check-inline">
                            <input 
                                class="custom-check-input" 
                                type="radio" 
                                v-model="formData.notSave.paymentMode" 
                                id="inlineRadio2" 
                                value="Mastercard" 
                                @input="resetError('paymentMode')"
                            >
                            <label class="form-check-label" for="inlineRadio2">Mastercard</label>
                        </div>
                        <div class="form-check form-check-inline">
                            <input 
                                class="custom-check-input" 
                                type="radio" 
                                v-model="formData.notSave.paymentMode" 
                                id="inlineRadio3" 
                                value="Amex" 
                                @input="resetError('paymentMode')"
                            >
                            <label class="form-check-label" for="inlineRadio3">Amex</label>
                        </div>
                    </div>
                    <div v-if="errors.paymentMode">
                        <small v-for="(err, i) in errors.paymentMode" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-5">
                    <label for="company" class="form-label fw-bold text-uppercase">
                        Company 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="text" 
                        class="form-control" 
                        id="company"
                        autocomplete="organization"
                        v-model="formData.save.company"
                        @input="resetError('company')"
                    >
                    <div v-if="errors.company">
                        <small v-for="(err, i) in errors.company" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-5">
                    <label for="card-number" class="form-label fw-bold text-uppercase">
                        Card number 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="text" 
                        class="form-control" 
                        id="card-number" 
                        placeholder="xxxx xxxx xxxx xxxx"
                        autocomplete="cc-number"
                        v-model="formData.notSave.cardNumber"
                        @keydown="controlKeyPressed"
                        @keyup.passive="reformatCardNumber"
                        @input="resetError('cardNumber')"
                    >
                    <div v-if="errors.cardNumber">
                        <small v-for="(err, i) in errors.cardNumber" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-5">
                    <label for="email" class="form-label fw-bold text-uppercase">
                        Email 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="email" 
                        class="form-control" 
                        id="email"
                        autocomplete="email"
                        v-model="formData.save.email"
                        @input="resetError('email')"
                    >
                    <div v-if="errors.email">
                        <small v-for="(err, i) in errors.email" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-5">
                    <label for="expiration" class="form-label fw-bold text-uppercase">
                        Expiration 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="month" 
                        class="form-control" 
                        id="expiration" 
                        :min="currentMonth"
                        autocomplete="cc-exp"
                        v-model="formData.notSave.expiration"
                        @input="resetError('expiration')"
                    >
                    <div v-if="errors.expiration">
                        <small v-for="(err, i) in errors.expiration" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-5">
                    <label for="phone" class="form-label fw-bold text-uppercase">
                        Phone number 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="tel" 
                        class="form-control" 
                        id="phone" 
                        autocomplete="tel"
                        v-model="formData.save.phone" 
                        @input="resetError('phone')"
                    >
                    <div v-if="errors.phone">
                        <small v-for="(err, i) in errors.phone" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-5">
                    <label for="cvn" class="form-label fw-bold text-uppercase">
                        Cvn 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="text" 
                        class="form-control" 
                        id="cvn" 
                        minlength="3" 
                        maxlength="3"
                        autocomplete="cc-csc"
                        v-model="formData.notSave.cvn"
                        @keydown="controlKeyPressed"
                        @input="resetError('cvn')"
                    >
                    <div v-if="errors.cvn">
                        <small v-for="(err, i) in errors.cvn" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group mb-4 px-5 mt-4">
                    <label for="donate" class="form-label fw-bold text-uppercase mb-3">
                        Donate us 
                        <span class="text-danger">*</span>
                    </label>
                    <RangeSlider :range="10000" :interval="10" @passValue="getDonationValue" />
                    <div v-if="errors.donationValue">
                        <small v-for="(err, i) in errors.donationValue" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>
            </div>
            <div class="text-end d-flex justify-content-md-end mt-4 px-5">
                <button type="submit" class="btn btn-success fw-bold my-btn">Submit</button>
                <button type="reset" class="btn btn-outline-secondary fw-bold my-btn">Reset</button>
            </div>
        </form>
    </div>
</template>

<script>
    import RangeSlider from '../components/RangeSlider.vue'

    const initialData = () => {
        return {
            formData: {
                save: {
                    firstName: '',
                    lastName: '',
                    company: '',
                    email: '',
                    phone: '',
                    gender: ''
                },
                notSave: {
                    paymentMode: '',
                    cardNumber: '',
                    expiration: '',
                    cvn: '',
                    donationValue: 0
                }
            },
            errors: {
                firstName: [],
                lastName: [],
                company: [],
                email: [],
                phone: [],
                gender: [],
                paymentMode: [],
                cardNumber: [],
                expiration: [],
                cvn: [],
                donationValue: [],
                total: 0
            }
        };
    };

    export default {
        components: { RangeSlider },
        data: initialData,
        mounted() {
            this.fetchData();
        },
        computed: {
            currentMonth() {
                const today = new Date();
                const mm = String(today.getMonth() + 1).padStart(2, '0');
                const yyyy = today.getFullYear();
                return `${yyyy}-${mm}`;
            }
        },
        watch: {
            'formData.notSave.donationValue': function() {
                this.resetError('donationValue');
            } 
        },
        methods: {
            fetchData() {
                if (localStorage.formData) {
                    const data = JSON.parse(localStorage.formData);
                    this.formData.save = data.save;
                }
            },
            getDonationValue(value) {
                this.formData.notSave.donationValue = value;
            },
            controlKeyPressed(e) {
                const keysAllowed = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'Backspace', 'Delete'];
                const keyPressed = e.key;
                if (!keysAllowed.includes(keyPressed)) {
                    e.preventDefault();
                }
            },
            formatName(e) {
                e.target.value = this.reformatWord(e.target.value);
            },
            reformatWord(word) {
                return word.toUpperCase()
                            .normalize('NFD')
                            .replace(/[\u0300-\u036f]/g, '')
                            .replace(/đ/g, 'd').replace(/Đ/g, 'D');
            },
            reformatCardNumber() {
                this.formData.notSave.cardNumber = this.formData.notSave.cardNumber.replace(/\s/g, '');
                const MAX_LENGTH = 19;
                for (let i = 4; i < this.formData.notSave.cardNumber.length && i < MAX_LENGTH; i += 5) {
                    this.formData.notSave.cardNumber = this.formData.notSave.cardNumber.slice(0, i) + ' ' + this.formData.notSave.cardNumber.slice(i);
                }
            },
            resetError(prop) {
                this.errors[prop] = [];
            },
            validate() {
                this.validRequiredData();
                this.validCardNumber();
            },
            validRequiredData() {
                for (const saveOption in this.formData) {
                    for (const prop in this.formData[saveOption]) {
                        if (!this.formData[saveOption][prop]) {
                            this.errors[prop].push(`${prop} must be required.`);
                            this.errors.total++;
                        }
                    }
                }
            },
            validCardNumber() {
                console.log(this.formData.notSave.cardNumber.length);
                if (this.formData.notSave.cardNumber &&
                    (this.formData.notSave.cardNumber.length < 13 ||
                    this.formData.notSave.cardNumber.length > 19)
                ) {
                    this.errors.cardNumber.push('Card number must be bigger than 12 and smaller than 20.');
                }
            },
            submit() {
                for (const prop in this.errors) {
                    if (prop !== 'total') {
                        this.errors[prop] = [];
                    }
                }
                this.errors.total = 0;
                this.formData.save.firstName = this.reformatWord(this.formData.save.firstName);
                this.formData.save.lastName = this.reformatWord(this.formData.save.lastName);
                this.validate();
                if (this.errors.total === 0) {
                    localStorage.formData = JSON.stringify({save: this.formData.save});
                    this.$router.push({name: 'success'});
                }
            },
            reset() {
                Object.assign(this.$data, initialData());
            }
        }
    }
</script>

<style>
    .my-btn {
        width: 9rem;
        height: 2.8rem;
        text-transform: uppercase;
        margin-left: 20px;
    }
    .custom-check-input {
        width: 1em;
        height: 1em;
        margin-right: 0.5em;
        accent-color: #319e5e;
    }
</style>
