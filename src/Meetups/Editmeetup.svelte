<script>
  import TextInput from "../UI/TextInput.svelte";
  import Button from "../UI/Button.svelte";
  import { createEventDispatcher } from "svelte";
  import Modal from "../UI/Modal.svelte";
  import { isEmpty } from "../helpers/validation.js";
  let title = "";
  let subtitle = "";
  let address = "";
  let email = "";
  let description = "";
  let imageUrl = "";
  let titleValid = false;
  $: titleValid = !isEmpty(title);
  const dispatch = createEventDispatcher();
  function submitForm() {
    dispatch("save", {
      id: Math.random().toString(),
      title: title,
      subtitle: subtitle,
      description: description,
      imageUrl: imageUrl,
      email: email,
      address: address
    });
  }
  function cancel() {
    dispatch("cancel");
  }
</script>

<style>
  form {
    width: 100%;
  }
</style>

<Modal title="Edit Meet Up" on:cancel>
  <form on:submit|preventDefault={submitForm}>
    <TextInput
      id="title"
      label="Title"
      value={title}
      valid={titleValid}
      validityMessage="Please enter a valid title"
      on:input={event => (title = event.target.value)} />
    <TextInput
      id="subtitle"
      label="Subtitle"
      value={subtitle}
      on:input={event => (subtitle = event.target.value)} />
    <TextInput
      id="address"
      label="Address"
      value={address}
      on:input={event => (address = event.target.value)} />
    <TextInput
      id="imageUrl"
      label="Image URL"
      value={imageUrl}
      on:input={event => (imageUrl = event.target.value)} />
    <TextInput
      id="email"
      label="E-Mail"
      type="email"
      value={email}
      on:input={event => (email = event.target.value)} />
    <TextInput
      id="description"
      label="Description"
      controlType="textarea"
      value={description}
      on:input={event => (description = event.target.value)} />
    <!-- -->
  </form>
  <div slot="footer">
    <Button type="button" mode="outline" on:click={cancel}>Cancel</Button>
    <Button type="button" on:click={submitForm}>Save</Button>
  </div>
</Modal>
