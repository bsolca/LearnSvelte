<script>
    import 'uikit';
    import ContactCard from './ContactCard.svelte';

    let username = "Benjamin";
    let jobTitle;
    let imageUrl;
    let description;
    let titleAge = 29;
    let password = "";
    let badPassword = false;
    let uppercaseName;
    let cardList = [];

    $: uppercaseName = username.toUpperCase();
    $: badPassword = password.length !== 0 && (password.length < 5 || password.length > 10);

    function changeAge() {
        titleAge += 1;
    }

    function removeCard(nb) {
        cardList = cardList.filter((elem, id) => {
            return id !== nb;
        })
    }

    function nameInput(event) {
        username = event.target.value;
    }

    function isExclamation() {
        return username.includes("!");
    }

    function addCard() {
        cardList = [
            ...cardList,
            {
                id: Math.random(),
                username: username,
                jobTitle: jobTitle,
                imageUrl: imageUrl,
                description: description,
                password: password,
            }
        ];
    }
</script>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }

    .blueColor {
        color: blue;
    }

    h1 {
        color: #ff3e00;
        font-size: 4em;
        font-weight: 100;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>

<main>
    <h1 class:blueColor={username.includes("!")}>Hello {uppercaseName} I am {titleAge}</h1>
    <button type="button" class="uk-button uk-button-default" on:click={changeAge}>Increase age</button>
    <div class="uk-section">
        <div class="uk-container">
            <form>
                <input class="uk-input uk-margin-small" title="Username" placeholder="Username" type="text"
                       bind:value={username} />
                <input class="uk-input uk-margin-small" title="Job title" placeholder="Job title" type="text"
                       bind:value={jobTitle} />
                <input class="uk-input uk-margin-small" title="Image URL" placeholder="Image URL" type="url"
                       bind:value={imageUrl} />
                <textarea class="uk-textarea uk-margin-small" title="Description" placeholder="Description"
                          bind:value={description}></textarea>
                <input class:uk-form-danger={badPassword} class:uk-form-success={!badPassword && password.length !== 0}
                       class="uk-input uk-margin-small" title="Password" placeholder="password" type="password"
                       bind:value={password} />
                {#if badPassword}
                    <div class="uk-alert-warning" uk-alert>
                        <b>You have {password.length} character(s)</b>
                        <p>Password must be between 5 and 10 characters</p>
                    </div>
                {/if}
                <button type="button" class="uk-button uk-button-primary uk-align-left uk-width-1-2 uk-margin-small"
                        on:click={addCard}>
                    Add Contact
                </button>
            </form>

        </div>
    </div>
    <div class="uk-section uk-container uk-padding-remove">
        {#if cardList.length === 0}
            <div class="uk-alert-primary uk-width-expand" uk-alert>
                <p>Add a card</p>
            </div>
        {/if}
        <div class="uk-grid-column-small uk-grid-row-medium uk-child-width-1-3@s  uk-margin-small" uk-grid>
            {#each cardList as contact, i (contact.id)}
                <div>
                    <ContactCard
                            username={contact.username}
                            jobTitle={contact.jobTitle}
                            description={contact.description}
                            imageUrl={contact.imageUrl}
                            password={contact.password}
                    />
                    <button class="uk-button-danger" on:click={removeCard.bind(this, i)}>Remove</button>
                </div>
            {/each}
        </div>
    </div>
</main>
