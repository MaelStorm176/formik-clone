<script setup>
import Field from "./components/Field.vue";
import Formik from "./components/Formik.vue";
import ErrorMessage from "./components/ErrorMessage.vue";

const onSubmit = (values) => {
  alert("Form submitted ! ");
};

const validate = (values) => {
  const errors = {};
  if (!values.email) {
    errors.email = "Required";
  } else if (!/\S+@\S+\.\S+/.test(values.email)) {
    errors.email = "Invalid email address";
  } else if (!values.password) {
    errors.password = "Required";
  }
  return errors;
};

const initialValues = {
  name: '',
  email: 'jamin.mael@orange.fr',
  password: '',
  phone: '0632542312',
  check: false,
  select: '1',
  submit: true
};
</script>

<template>
  <header>
    <h1>Formik Clone</h1>
  </header>

  <main>
    <Formik
      :initialValues="initialValues"
      :onSubmit="onSubmit"
      :validate="validate"
      style="display: flex; flex-direction: column; gap: 1rem; width: 50%; margin: 0 auto;"
    >

      <label for="name">Name</label>
      <Field name="name" as="input" type="text" placeholder="Name" />

      <label for="email">Email</label>
      <Field name="email" as="input" type="email" placeholder="Email" />
      <ErrorMessage name="email" as="span" style="color: red" />

      <label for="password">Password</label>
      <Field name="password" as="input" type="password" placeholder="Password" />
      <ErrorMessage name="password" as="span" style="color: purple" />

      <label for="phone">Phone</label>
      <Field name="phone" as="input" type="tel" placeholder="Tel. Number" />

      <label for="check">Checkbox</label>
      <Field name="check" as="input" type="checkbox"/>

      <label for="select">Select a number</label>
      <Field name="select" as="select">
        <option value="1">One</option>
        <option value="2">Two</option>
        <option value="3">Three</option>
      </Field>
      <Field as="button" type="submit" name="submit" style="width: 100%">
        Submit
      </Field>
    </Formik>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
