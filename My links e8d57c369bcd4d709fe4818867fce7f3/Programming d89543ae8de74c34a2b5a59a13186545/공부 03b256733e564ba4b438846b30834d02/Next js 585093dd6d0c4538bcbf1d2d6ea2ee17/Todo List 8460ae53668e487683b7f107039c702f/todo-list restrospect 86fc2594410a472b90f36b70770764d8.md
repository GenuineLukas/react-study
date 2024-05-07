# todo-list restrospect

The main technology used here is Next.js’ Server Actions feature.

Server Actions are asynchronous functions that are executed on the server. They can be used in Srver and Client Components to handle form submissions and data mutation in Next.js applications. 

You can use server actions instead of HTTP requests to pass data from client-side componetns to server-sid functions and back.

This simplifies your code because instead of building a bunch of HTTP requests for stuff you can't do client-side (database queries, etc), you just import a function and call that function. The `'use server'` declaration at the top of your server action ensures that nothing from your server action leaks into the client side, so your ENV variables and secrets are safe. Also, http cookies get passed to your server action, so you can easily identify who is calling the function!