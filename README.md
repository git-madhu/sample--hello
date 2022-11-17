# sample--hello

[you](https://learn.microsoft.com/en-us/azure/active-directory/manage-apps/what-is-access-management#requiring-user-assignment-for-an-app){:target="_blank"}


# Some markdown
*click below*
<a href="https://learn.microsoft.com/en-us/azure/active-directory/manage-apps/what-is-access-management#requiring-user-assignment-for-an-app" target="_blank">New Tab</a>
...

<a href="[http://example.com](https://learn.microsoft.com/en-us/azure/active-directory/manage-apps/what-is-access-management#requiring-user-assignment-for-an-app)/" target="_blank">Hello, world!</a>

function LinkRenderer(props) {
  return <a href={props.href} target="_blank">{props.children}</a>
}

<ReactMarkdown
  source="Click [here]([https://espen.codes/](http://example.com](https://learn.microsoft.com/en-us/azure/active-directory/manage-apps/what-is-access-management#requiring-user-assignment-for-an-app)) to visit external site"
  renderers={{link: LinkRenderer}}
/>
