<script setup lang="ts">
import { toTypedSchema } from "@vee-validate/zod";
import { configure, useForm } from "vee-validate";
import { z } from "zod";

const schema = toTypedSchema(
  z.object({ name: z.string().min(10), surname: z.string().min(10) })
);

const { defineField, handleSubmit, errors, defineInputBinds } = useForm({
  validationSchema: schema,
});

configure({
  validateOnChange: false,
  validateOnModelUpdate: false,
});

const [name, nameAttrs] = defineField("name");
const surname = defineInputBinds("surname");

const handleSubmitClicked = handleSubmit((values) => {
  console.log(values);
});
</script>

<template>
  <Form @click="handleSubmitClicked" :validation-schema="schema">
    <div>
      <input v-bind="nameAttrs" v-model="name" placeholder="name" />

      <span v-if="errors.name">{{ errors.name }}</span>
    </div>
    <div>
      <input v-bind="surname" placeholder="surname" />

      <span v-if="errors.surname">{{ errors.surname }}</span>
    </div>

    <button type="submit">submit</button>
  </Form>
</template>
