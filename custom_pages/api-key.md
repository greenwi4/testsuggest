---
title: api key
fullscreen: false
hidden: false
---
<HTMLBlock>{`
<style>
    .Content-Wrapper { padding: 1em; }
    .Title { text-align: center; padding: 2em 0; }
    .Content {
        padding: 2em;
        border-radius: 30px 30px 0 30px;
        background-color: #fff;
    }
    .boldLabel { font-weight: bold; }
    .inline_div { margin-bottom: 0.5em; }

    #ebslogin,
    #generate-secret,
    #copy-client-secret,
    #copy-client-id {
        background-color: #258AD6;
        border: none;
        color: white;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 14px;
        margin: 4px 2px;
        cursor: pointer;
        height: 32px;
        width: 100px;
        border-radius: 5px;
    }
    #ebscancel,
    #cancelButton {
        background-color: #fff;
        border: solid 1px #258AD6;
        color: #258AD6;
        display: inline-block;
        font-size: 14px;
        margin: 4px 2px;
        cursor: pointer;
        height: 32px;
        width: 100px;
        border-radius: 5px;
    }
    #generate-secret { width: 150px !important; }

    input {
        display: inline-block;
        background-color: #fff;
        border: solid 1px #a9b1be;
        width: 70%;
        height: 30px;
        color: black;
        margin-bottom: 10px;
        padding: 0 8px;
    }

    #subsection { display: none; }
    #table-div { padding-left: 25%; }

    /* Confirmation modal */
    .container { max-width: 600px; margin: 0 auto; }
    .wrapper   { max-height: 80px; border-radius: 5px; }
    .msg-text  {
        width: 412px; height: 20px;
        font-family: ProximaNova; font-size: 16px;
        text-align: center; color: #697489;
    }
    .btn-ok {
        width: 156px; height: 28px; border-radius: 2px;
        background-color: #2080cd; border: solid 1px #006aa9;
        margin: 15px 0 0 10px;
    }
    .btn-cancel {
        width: 156px; height: 28px; border-radius: 2px;
        background-color: #fff; border: solid 1px #a8b1be;
        margin-top: 15px;
    }
    .btn-ok-text     { font-size: 13px; font-weight: 600; color: #fff; }
    .btn-cancel-text { font-size: 13px; font-weight: 600; color: #2080cd; }

    @media only screen and (max-width: 500px) {
        #table-div { padding-left: 0; }
        input      { width: 100% !important; }
    }
</style>

<div id="divApiKey">
    <div id="api-wrapper">
        <div class="Content-Wrapper">

            <div class="Title" id="mainsection">
                <p id="ebs-login-message">
                    Encompass "super admin" credentials are required to view the API Key.
                    Please sign in to Encompass.
                </p>
                <button id="ebslogin"  class="btn" type="button">Sign In</button>
                <button id="ebscancel" class="btn" type="button">Cancel</button>
            </div>

            <div class="Content" id="subsection">
                <div id="table-div">
                    <div id="message-board">
                        <div id="apikey-error"   style="color: red;"></div>
                        <div id="apikey-message" style="color: blue;">Loading…</div>
                    </div>

                    <div>
                        <div class="boldLabel">Client ID (OAuth):</div>
                        <div class="inline_div">
                            <span><input id="client-id" value="" disabled /></span>
                            <span><button type="button" id="copy-client-id">Copy</button></span>
                        </div>
                    </div>

                    <br />

                    <div>
                        <div class="boldLabel">Client Secret:</div>
                        <div class="inline_div">
                            <span>
                                <input type="hidden" id="client-secret" value="" />
                                <input id="client-secret-mask" value="" disabled />
                            </span>
                            <span><button type="button" id="copy-client-secret">Copy</button></span>
                        </div>
                    </div>

                    <div>
                        <button type="button" id="cancelButton">Cancel</button>
                        <button type="button" id="generate-secret" style="display:none;">Regenerate Secret</button>
                    </div>
                </div>
            </div>

        </div>
    </div>
</div>
`}</HTMLBlock>

<br />
