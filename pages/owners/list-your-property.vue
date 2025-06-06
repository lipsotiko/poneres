<template>
    <IToast v-if="saved" v-model="saved" color="success" dismissible>
        <p>Your request has been submitted. Our team will be in touch with you soon.</p>
    </IToast>
    <IContainer>
        <div class="top">
            <h3>List your property</h3>
        </div>
        <div>
            <p class="lead">
                Before listing your property for sale, we will work with you to develop a unique marketing strategy
                aimed at selling your home quickly and for the highest possible price. You'll receive a comprehensive
                market analysis based on recently sold properties similar in features and condition to your home in the
                local area. This will help determine the optimal sale price, ensuring a quick sale while maximizing your
                profit.
            </p>
        </div>
        <ClientOnly>
            <IForm v-model="schema" @update:modelValue="handleFormUpdate">
                <div v-if="saved" class="form-container">
                    <IRow>
                        <IColumn>
                            <div class="request-sent">
                                <p class="lead">Thank you for contacting us!</p>
                            </div>
                        </IColumn>
                    </IRow>
                </div>
                <div v-else class="form-container">
                    <IRow>
                        <IColumn xs="12" sm="6">
                            <IFormGroup required>
                                <IFormLabel for="firstName">First name</IFormLabel>
                                <IInput name="firstName" autocomplete :error="errorTypes" />
                                <IFormError for="firstName" :visible="errorTypes" />
                            </IFormGroup>
                        </IColumn>
                        <IColumn xs="12" sm="6">
                            <IFormGroup required>
                                <IFormLabel for="lastName">Last name</IFormLabel>
                                <IInput name="lastName" autocomplete :error="errorTypes" />
                                <IFormError for="lastName" :visible="errorTypes" />
                            </IFormGroup>
                        </IColumn>
                    </IRow>
                    <IRow>
                        <IColumn xs="12" sm="6">
                            <IFormGroup required>
                                <IFormLabel for="email">E-mail address</IFormLabel>
                                <IInput name="email" autocomplete :error="errorTypes" />
                                <IFormError for="email" :visible="errorTypes" />
                            </IFormGroup>
                        </IColumn>
                        <IColumn xs="12" sm="6">
                            <IFormGroup required>
                                <IFormLabel for="phone">Phone number</IFormLabel>
                                <IInput name="phone" autocomplete :error="errorTypes" />
                                <IFormError for="phone" :visible="errorTypes" />
                            </IFormGroup>
                        </IColumn>
                    </IRow>
                    <IRow>
                        <IColumn xs="12">
                            <IFormGroup required>
                                <IFormLabel for="address">Property address</IFormLabel>
                                <IInput name="address" autocomplete :error="errorTypes" />
                                <IFormError for="address" :visible="errorTypes" />
                            </IFormGroup>
                        </IColumn>
                    </IRow>
                    <IRow>
                        <IColumn xs="12">
                            <IFormGroup>
                                <IFormLabel for="additional">Additional information</IFormLabel>
                                <ITextarea name="additional" autocomplete :error="errorTypes" />
                                <IFormError for="additional" :visible="errorTypes" />
                            </IFormGroup>
                        </IColumn>
                    </IRow>
                    <p>* Your information will not be shared with a third party.</p>
                    <IRow>
                        <IColumn>
                            <div class="create-request">
                                <div>
                                    <IButton color="light" size="lg" :loading="saving" @click="submitRequest"
                                        :disabled="!schema.touched || schema.invalid">
                                        Submit</IButton>
                                    <IButton outline color="dark" size="lg" @click="clear" :disabled="saving">
                                        Clear</IButton>
                                </div>
                            </div>
                        </IColumn>
                    </IRow>
                </div>
            </IForm>
        </ClientOnly>
    </IContainer>
</template>
<script setup>
import { AsYouType } from 'libphonenumber-js'
import { useForm } from "@inkline/inkline/composables";

useHead({
    titleTemplate: "List your property | %s",
});

const runtimeConfig = useRuntimeConfig()
const saving = ref(false);
const saved = ref(false);

const handleFormUpdate = async (e) => {
    if (!e.phone.value) {
        return;
    }
    const formatted = new AsYouType('US').input(e.phone.value);
    schema.value.phone.value = formatted
}

const { schema } = useForm({
    email: {
        validators: [
            {
                name: "required",
            },
            {
                name: "custom",
                message: "Please enter a valid email address.",
                validator: emailValidator,
            },
        ],
    },
    firstName: { validators: [{ name: "required" }] },
    lastName: { validators: [{ name: "required" }] },
    phone: {
        validators: [
            { name: "required" },
            {
                name: "custom",
                message: "Please enter a valid phone number",
                validator: (v) => {
                    return /\([0-9]{3}\) [0-9]{3}-[0-9]{4}$/.test(v)
                }
            }
        ]
    },
    address: { validators: [{ name: "required" }] },
    additional: {}
});

const errorTypes = ["touched", "invalid"];
const successfulSubmission = ref(false);

const clear = () => {
    schema.value.firstName.value = ''
    schema.value.lastName.value = ''
    schema.value.email.value = ''
    schema.value.phone.value = ''
    schema.value.address.value = ''
    schema.value.additional.value = ''
}

const submitRequest = async () => {
    saving.value = true;

    await $fetch(`/api/public/contact/request`, {
        baseURL: runtimeConfig.public.apiBase,
        method: "POST",
        mode: 'no-cors',
        headers: {
            'Content-Type': 'x-www-form-urlencoded',
        },
        body: new URLSearchParams({
            'firstName': schema.value.firstName.value,
            'lastName': schema.value.lastName.value,
            'email': schema.value.email.value,
            'phone': schema.value.phone.value,
            'message': `I would like to list my property for sale: ${schema.value.address.value} ${schema.value.additional.value}`
        })
    }).then(() => {
        clear();
        saving.value = false;
        saved.value = true;
    });
};
</script>
<style scoped>
.lead {
    padding: 38px;
    margin-bottom: 0;
}

.create-request {
    margin-top: 48px;
    text-align: center;
    margin-bottom: 200px;
}

.create-request button {
    margin: 12px;
    width: 188px;
}

.request-sent {
    text-align: center;
}

.form-container {
    margin: 0 22px;
}

.column {
    margin: 3px 0;
}
</style>