<script setup lang="ts">
import { toTypedSchema } from "@vee-validate/zod";
import { ErrorMessage, Field, Form, configure, useForm } from "vee-validate";
import { z } from "zod";

const schema = toTypedSchema(
  z.object({ name: z.string().length(2), surname: z.string().length(3) })
);

const { defineField, handleSubmit, errors } = useForm({
  validationSchema: schema,
});

configure({
  validateOnModelUpdate: false,
  validateOnChange: false,
  validateOnInput: false,
  validateOnBlur: false,
});

const [name, nameAttrs] = defineField("name", {
  validateOnModelUpdate: false,
  validateOnBlur: false,
  validateOnChange: false,
  validateOnInput: false,
});

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
      <Field name="surname" type="string" placeholder="surname" />

      <ErrorMessage name="surname" />
    </div>

    <button type="submit">submit</button>
  </Form>
</template>
