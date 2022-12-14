<script setup>
import Field from "./components/Field.vue";
import Formik from "./components/Formik.vue";

const onSubmit = (values) => {
  console.log(values);
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
</script>

<template>
  <header>
    <h1>My App</h1>
  </header>

  <main>
    <Formik
      :initialValues="{ name: '', email: 'jamin.mael@orange.fr', password: '', phone: '0632542312', check: false, select: '1' }"
      :onSubmit="onSubmit"
      :validate="validate"
    >
      <Field name="name" as="text" label="Name"/>
      <Field name="email" as="email" label="Email" />
      <Field name="password" as="password" label="Password" />
      <Field name="phone" as="tel" label="Phone" />
      <Field name="check" as="checkbox" label="Check" />
      <Field name="select" as="select" label="Select">
        <option value="1">One</option>
        <option value="2">Two</option>
        <option value="3">Three</option>
      </Field>
      <button type="submit">Submit</button>
    </Formik>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
