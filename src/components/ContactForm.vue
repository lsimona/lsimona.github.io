<script setup>
import { reactive, ref } from 'vue'

const props = defineProps({
  kind: {
    type: String,
    default: 'booking',
  },
})

const endpoint = 'https://formspree.io/ssimonanomiss@gmail.com'
const isBooking = props.kind === 'booking'
const isSending = ref(false)
const status = ref('')
const statusType = ref('')

const fields = reactive({
  name: '',
  email: '',
  contact: 'Skype',
  payment: 'Карта Российского банка',
  subject: '',
  message: '',
  privacy: false,
})

function resetForm() {
  fields.name = ''
  fields.email = ''
  fields.contact = 'Skype'
  fields.payment = 'Карта Российского банка'
  fields.subject = ''
  fields.message = ''
  fields.privacy = false
}

async function submitForm() {
  status.value = ''

  if (!fields.privacy) {
    statusType.value = 'error'
    status.value = 'Подтвердите согласие на обработку данных.'
    return
  }

  isSending.value = true
  const payload = new FormData()
  payload.append('name', fields.name)
  payload.append('email', fields.email)
  payload.append('_replyto', fields.email)
  payload.append('_subject', isBooking ? 'Новая запись на консультацию' : 'Новый вопрос с сайта')
  payload.append('message', fields.message)
  payload.append('privacy_consent', 'yes')

  if (isBooking) {
    payload.append('contact', fields.contact)
    payload.append('payment', fields.payment)
  } else {
    payload.append('subject', fields.subject)
  }

  try {
    const response = await fetch(endpoint, {
      method: 'POST',
      body: payload,
      headers: { Accept: 'application/json' },
    })

    if (!response.ok) throw new Error('Form request failed')

    statusType.value = 'success'
    status.value = 'Спасибо! Сообщение отправлено. Я свяжусь с вами в ближайшее время.'
    resetForm()
  } catch {
    statusType.value = 'error'
    status.value = 'Не удалось отправить форму. Напишите мне напрямую в Skype: simona7997.'
  } finally {
    isSending.value = false
  }
}
</script>

<template>
  <form class="contact-form" :action="endpoint" method="post" @submit.prevent="submitForm">
    <input type="hidden" name="_subject" :value="isBooking ? 'Новая запись на консультацию' : 'Новый вопрос с сайта'" />

    <div class="form-grid">
      <label>
        <span>Ваше имя</span>
        <input v-model.trim="fields.name" name="name" type="text" autocomplete="name" placeholder="Например, Анна" required />
      </label>
      <label>
        <span>Email</span>
        <input v-model.trim="fields.email" name="email" type="email" autocomplete="email" placeholder="you@example.com" required />
      </label>
    </div>

    <template v-if="isBooking">
      <div class="form-grid">
        <label>
          <span>Как связаться</span>
          <select v-model="fields.contact" name="contact" required>
            <option>Skype</option>
            <option>Telegram</option>
            <option>WhatsApp</option>
          </select>
        </label>
        <label>
          <span>Способ оплаты</span>
          <select v-model="fields.payment" name="payment" required>
            <option>Карта Российского банка</option>
            <option>Карта Белорусского банка</option>
            <option>Другой способ</option>
          </select>
        </label>
      </div>
    </template>

    <label v-else>
      <span>Тема</span>
      <input v-model.trim="fields.subject" name="subject" type="text" placeholder="О чём вы хотите спросить?" required />
    </label>

    <label>
      <span>{{ isBooking ? 'Коротко опишите вашу ситуацию' : 'Сообщение' }}</span>
      <textarea v-model.trim="fields.message" name="message" rows="5" :placeholder="isBooking ? 'Что сейчас происходит и какой помощи вы ждёте?' : 'Ваш вопрос'" required></textarea>
    </label>

    <label class="checkbox-label">
      <input v-model="fields.privacy" type="checkbox" required />
      <span>Соглашаюсь на обработку персональных данных для ответа на сообщение.</span>
    </label>

    <button class="button button-primary" type="submit" :disabled="isSending" :aria-busy="isSending">
      {{ isSending ? 'Отправляю…' : isBooking ? 'Записаться на консультацию' : 'Отправить вопрос' }}
    </button>

    <p v-if="status" class="form-status" :class="`form-status-${statusType}`" role="status">{{ status }}</p>
  </form>
</template>
