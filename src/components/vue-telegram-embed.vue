<template>
  <iframe
    frameborder="0"
    scrolling="no"
    v-bind:width="width"
    v-bind:src="src"
    v-bind:id="id"
    v-bind:height="height"
    ref="iframe"
  />
</template>

<script>
export default {
  name: "TelegramEmbed",
  props: {
    link: {
      type: String,
      required: true
    },
    width: {
      type: String,
      default: "100%"
    },
    userpic: {
      type: String,
      default: "auto",
      validator: function(value) {
        return ["true", "false", "auto"].indexOf(value) !== -1;
      }
    },
    single: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      height: "80px"
    };
  },
  mounted() {
    window.addEventListener("message", this.messageHandler);

    this.$refs.iframe.addEventListener("load", () => {
      this.checkFrame(this.id);
    });
  },
  beforeDestroy() {
    window.removeEventListener("message", this.messageHandler);
  },
  computed: {
    userpicAttr: function() {
      let str = "";
      switch (this.userpic) {
        case "true":
        case "false":
          str = `userpic=${this.userpic}`;
          break;
        case "auto":
        case "default":
      }
      return str;
    },
    singleAttr: function() {
      if (this.single) return "single";
      return "";
    },
    src: function() {
      return (
        "https://t.me/" +
        this.link +
        "?embed=1&" +
        [this.userpicAttr, this.singleAttr].filter(e => e).join("&")
      );
    },
    id: function() {
      return "telegram-post-" + this.link.replace(/[^a-z0-9_]/gi, "-");
    }
  },
  methods: {
    messageHandler(event) {
      this.resize(event);
    },
    checkFrame(id) {
      this.$refs.iframe.contentWindow.postMessage(
        JSON.stringify({ event: "visible", frame: id }),
        "*"
      );
    },
    resize({ data, source }) {
      if (
        !data ||
        typeof data !== "string" ||
        source !== this.$refs.iframe.contentWindow
      )
        return;

      const action = JSON.parse(data);

      if (action.event === "resize" && action.height) {
        this.height = action.height + "px";
      }
    }
  }
};
</script>

<style scoped>
iframe {
  border: none;
  overflow: hidden;
  min-width: 320px;
}
</style>
