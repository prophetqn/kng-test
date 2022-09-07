<template>
    <div class="container">
        <form @submit.prevent="submit" @reset.prevent="reset" class="mx-0 mx-lg-5">
            <div class="row">
                <div class="form-group col-md-6 mb-4 px-4 px-lg-5">
                    <label for="first-name" class="form-label fw-bold text-uppercase">
                        First name 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="text" 
                        class="form-control py-3"
                        :class="{ 'is-valid': formData.firstName.valid === true, 'is-invalid': formData.firstName.valid === false }"
                        id="first-name" 
                        autocomplete="given-name"
                        v-model="formData.firstName.value" 
                        @keyup="formatName"
                        @input="resetError('firstName')"
                    >
                    <div v-if="errors.firstName">
                        <small v-for="(err, i) in errors.firstName" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-4 px-lg-5">
                    <label for="gender" class="form-label fw-bold text-uppercase">
                        Gender 
                        <span class="text-danger">*</span>
                    </label>
                    <select 
                        class="form-select py-3"
                        :class="{ 'is-valid': formData.gender.valid === true, 'is-invalid': formData.gender.valid === false }" 
                        id="gender" 
                        v-model="formData.gender.value" 
                        @input="resetError('gender')"
                    >
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

                <div class="form-group col-md-6 mb-4 px-4 px-lg-5">
                    <label for="last-name" class="form-label fw-bold text-uppercase">
                        Last name 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="text" 
                        class="form-control py-3" 
                        :class="{ 'is-valid': formData.lastName.valid === true, 'is-invalid': formData.lastName.valid === false }"
                        id="last-name" 
                        autocomplete="family-name"
                        v-model="formData.lastName.value" 
                        @keyup="formatName" 
                        @input="resetError('lastName')"
                    >
                    <div v-if="errors.lastName">
                        <small v-for="(err, i) in errors.lastName" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-4 px-lg-5">
                    <label class="form-label fw-bold text-uppercase">
                        Payment mode 
                        <span class="text-danger">*</span>
                    </label>
                    <div>
                        <div class="form-check-inline d-inline-flex align-items-center lh-lg c-mr">
                            <input 
                                class="c-check-input" 
                                type="radio" 
                                v-model="formData.paymentMode.value" 
                                id="inlineRadio1" 
                                value="Visa" 
                                @input="resetError('paymentMode')"
                            >
                            <label class="form-check-label c-semibold" for="inlineRadio1">Visa</label>
                        </div>
                        <div class="form-check-inline d-inline-flex align-items-center lh-lg c-mr">
                            <input 
                                class="c-check-input" 
                                type="radio" 
                                v-model="formData.paymentMode.value" 
                                id="inlineRadio2" 
                                value="Mastercard" 
                                @input="resetError('paymentMode')"
                            >
                            <label class="form-check-label c-semibold" for="inlineRadio2">Mastercard</label>
                        </div>
                        <div class="form-check-inline d-inline-flex align-items-center lh-lg c-mr">
                            <input 
                                class="c-check-input" 
                                type="radio" 
                                v-model="formData.paymentMode.value" 
                                id="inlineRadio3" 
                                value="Amex" 
                                @input="resetError('paymentMode')"
                            >
                            <label class="form-check-label c-semibold" for="inlineRadio3">Amex</label>
                        </div>
                    </div>
                    <div v-if="errors.paymentMode">
                        <small v-for="(err, i) in errors.paymentMode" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-4 px-lg-5">
                    <label for="company" class="form-label fw-bold text-uppercase">
                        Company 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="text" 
                        class="form-control py-3" 
                        :class="{ 'is-valid': formData.company.valid === true, 'is-invalid': formData.company.valid === false }"
                        id="company"
                        autocomplete="organization"
                        v-model="formData.company.value"
                        @input="resetError('company')"
                    >
                    <div v-if="errors.company">
                        <small v-for="(err, i) in errors.company" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-4 px-lg-5">
                    <label for="card-number" class="form-label fw-bold text-uppercase">
                        Card number 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="text" 
                        class="form-control py-3" 
                        :class="{ 'is-valid': formData.cardNumber.valid === true, 'is-invalid': formData.cardNumber.valid === false }"
                        id="card-number" 
                        placeholder="xxxx xxxx xxxx xxxx"
                        autocomplete="cc-number"
                        maxlength="19"
                        v-model="formData.cardNumber.value"
                        @keydown="controlCardNumberPressed"
                        @keyup.passive="reformatCardNumber"
                        @input="resetError('cardNumber')"
                    >
                    <div v-if="errors.cardNumber">
                        <small v-for="(err, i) in errors.cardNumber" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-4 px-lg-5">
                    <label for="email" class="form-label fw-bold text-uppercase">
                        Email 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="email" 
                        class="form-control py-3" 
                        :class="{ 'is-valid': formData.email.valid === true, 'is-invalid': formData.email.valid === false }"
                        id="email"
                        autocomplete="email"
                        v-model="formData.email.value"
                        @input="resetError('email')"
                    >
                    <div v-if="errors.email">
                        <small v-for="(err, i) in errors.email" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-4 px-lg-5">
                    <label for="expiration" class="form-label fw-bold text-uppercase">
                        Expiration 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="month" 
                        class="form-control py-3" 
                        :class="{ 'is-valid': formData.expiration.valid === true, 'is-invalid': formData.expiration.valid === false }"
                        id="expiration" 
                        :min="currentMonth"
                        autocomplete="cc-exp"
                        v-model="formData.expiration.value"
                        @input="resetError('expiration')"
                    >
                    <div v-if="errors.expiration">
                        <small v-for="(err, i) in errors.expiration" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-4 px-lg-5">
                    <label for="phone" class="form-label fw-bold text-uppercase">
                        Phone number 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="tel" 
                        class="form-control py-3" 
                        :class="{ 'is-valid': formData.phone.valid === true, 'is-invalid': formData.phone.valid === false }"
                        id="phone" 
                        autocomplete="tel"
                        v-model="formData.phone.value"
                        @keydown="controlPhoneNumberPressed"
                        @input="resetError('phone')"
                    >
                    <div v-if="errors.phone">
                        <small v-for="(err, i) in errors.phone" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group col-md-6 mb-4 px-4 px-lg-5">
                    <label for="cvn" class="form-label fw-bold text-uppercase">
                        Cvn 
                        <span class="text-danger">*</span>
                    </label>
                    <input 
                        type="text" 
                        class="form-control py-3" 
                        :class="{ 'is-valid': formData.cvn.valid === true, 'is-invalid': formData.cvn.valid === false }"
                        id="cvn" 
                        minlength="3" 
                        maxlength="3"
                        autocomplete="cc-csc"
                        v-model="formData.cvn.value"
                        @keydown="controlCardNumberPressed"
                        @input="resetError('cvn')"
                    >
                    <div v-if="errors.cvn">
                        <small v-for="(err, i) in errors.cvn" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>

                <div class="form-group mb-4 px-4 px-lg-5 mt-4">
                    <label for="donate" class="form-label fw-bold text-uppercase mb-3">
                        Donate us 
                        <span class="text-danger">*</span>
                    </label>
                    <RangeSlider :range="1000" :interval="5" @passValue="getDonation" />
                    <div v-if="errors.donation">
                        <small v-for="(err, i) in errors.donation" :key="i" class="d-block text-danger">
                            {{ err }}
                        </small>
                    </div>
                </div>
            </div>
            <div class="d-flex justify-content-md-end mt-4 px-4 px-lg-5">
                <button type="submit" class="btn btn-success fw-bold c-btn c-btn-green">Submit</button>
                <button type="reset" class="btn btn-outline-secondary fw-bold c-btn c-btn-gray">Reset</button>
            </div>
        </form>
    </div>
</template>

<script>
    import RangeSlider from '../components/RangeSlider.vue'

    const initialData = () => {
        return {
            formData: {
                firstName: {
                    value: '',
                    save: true,
                    valid: null,
                    rules: ['required', 'max:255']
                },
                lastName: {
                    value: '',
                    save: true,
                    valid: null,
                    rules: ['required', 'max:255']
                },
                company: {
                    value: '',
                    save: true,
                    valid: null,
                    rules: ['required', 'max:255']
                },
                email: {
                    value: '',
                    save: true,
                    valid: null,
                    rules: ['required', 'max:255', 'email']
                },
                phone: {
                    value: '',
                    save: true,
                    valid: null,
                    rules: ['required', 'max:255']
                },
                gender: {
                    value: '',
                    save: true,
                    valid: null,
                    rules: ['required']
                },
                paymentMode: {
                    value: '',
                    save: false,
                    valid: null,
                    rules: ['required']
                },
                cardNumber: {
                    value: '',
                    save: false,
                    valid: null,
                    rules: ['required', 'max:19']
                },
                expiration: {
                    value: '',
                    save: false,
                    valid: null,
                    rules: ['required']
                },
                cvn: {
                    value: '',
                    save: false,
                    valid: null,
                    rules: ['required', 'max:3']
                },
                donation: {
                    value: 0,
                    save: false,
                    valid: null,
                    rules: ['required']
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
                donation: [],
                total: 0
            }
        };
    };

    export default {
        components: { RangeSlider },
        data: initialData,
        mounted() {
            this.fetchDataFromLocal();
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
            'formData.donation.value': function() {
                this.resetError('donation');
            }
        },
        methods: {
            fetchDataFromLocal() {
                if (localStorage.formData) {
                    const data = JSON.parse(localStorage.formData);
                    for (const prop in data) {
                        if (data[prop] && Object.hasOwn(this.formData, prop)) {
                            this.formData[prop].value = data[prop].value;
                        }
                    }
                }
            },
            saveDataToLocal() {
                const saveData = {};
                for (const prop in this.formData) {
                    if (this.formData[prop].save) {
                        saveData[prop] = {};
                        saveData[prop].value = this.formData[prop].value;
                    }
                }
                localStorage.formData = JSON.stringify(saveData);
            },
            getDonation(value) {
                this.formData.donation.value = value;
            },
            controlCardNumberPressed(e) {
                const keysAllowed = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'Backspace', 'Delete'];
                const keyPressed = e.key;
                if (!keysAllowed.includes(keyPressed)) {
                    e.preventDefault();
                }
            },
            controlPhoneNumberPressed(e) {
                const keysAllowed = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '+', '.', '-', ' ', 'Backspace', 'Delete'];
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
                this.formData.cardNumber.value = this.formData.cardNumber.value.replace(/\s/g, '');
                const MAX_LENGTH = 19;
                for (let i = 4; i < this.formData.cardNumber.value.length && i < MAX_LENGTH; i += 5) {
                    this.formData.cardNumber.value = this.formData.cardNumber.value.slice(0, i) + ' ' + this.formData.cardNumber.value.slice(i);
                }
            },
            resetError(prop) {
                this.errors[prop] = [];
                this.formData[prop].valid = null;
            },
            validate() {
                this.validRequiredData();
                this.validCardNumber();
            },
            validRequiredData() {
                for (const prop in this.formData) {
                    if (!this.formData[prop].value) {
                        this.addError(prop, `${prop} must be required.`);
                    } else {
                        this.formData[prop].valid = true;
                    }
                }
            },
            validCardNumber() {
                if (this.formData.cardNumber.value &&
                    (this.formData.cardNumber.value.length < 13 ||
                    this.formData.cardNumber.value.length > 19)
                ) {
                    this.addError('cardNumber', 'Card number must be bigger than 12 and smaller than 20.');
                }
            },
            addError(prop, mess) {
                this.errors[prop].push(mess);
                this.errors.total++;
                this.formData[prop].valid = false;
            },
            submit() {
                for (const prop in this.errors) {
                    if (prop !== 'total') {
                        this.errors[prop] = [];
                    }
                }
                this.errors.total = 0;
                this.formData.firstName.value = this.reformatWord(this.formData.firstName.value);
                this.formData.lastName.value = this.reformatWord(this.formData.lastName.value);
                this.validate();
                if (this.errors.total === 0) {
                    this.saveDataToLocal();
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
    .c-btn {
        text-transform: uppercase;
        width: 10rem;
        margin-left: 2rem;
        padding-top: 0.8rem !important;
        padding-bottom: 0.8rem !important;
    }
    .c-btn-green {
        background-color: #319e5e !important;
    }
    .c-btn-green:hover {
        background-color: #2c8c54 !important;
    }
    .c-btn-gray {
        border: 0.2rem solid #ebebeb !important;
    }
    .c-check-input {
        width: 1.2rem;
        height: 1.2rem;
        margin-right: 0.5rem;
        accent-color: #319e5e;
    }
    .c-mr {
        margin-right: 2rem !important;
        height: 3.5rem !important;
    }
    .c-semibold {
        font-weight: 500;
    }
</style>
