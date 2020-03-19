<script>
    export let username;
    export let jobTitle;
    export let imageUrl;
    export let description;
    export let password;
</script>

<style>

</style>

<div>
    <div class="uk-card uk-card-default uk-card-body">
        <div class="uk-card-header">
            <div class="uk-grid-small uk-flex-middle" uk-grid>
                <div class="uk-width-auto">
                    <img class="uk-border-circle" width="40" height="40" src={imageUrl} alt={username}>
                </div>
                <div class="uk-width-expand">
                    <h3 class="uk-card-title uk-margin-remove-bottom">{username}</h3>
                    <p class="uk-text-meta uk-margin-remove-top">{jobTitle}</p>
                </div>
            </div>
        </div>
        <div class="uk-card-body">
            <p>{description}</p>
            <p>Password is: <b>{password}</b></p>
        </div>
    </div>
</div>
