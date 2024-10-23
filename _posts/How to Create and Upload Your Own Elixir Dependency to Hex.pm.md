# How to Create and Upload Your Own Elixir Dependency to Hex.pm

Creating and publishing your own Elixir package to [Hex.pm](https://hex.pm) can seem daunting at first, but it’s actually quite simple. In this guide, I’ll walk you through the steps of setting up your own dependency, registering an account on Hex, and publishing your package so that others can use it in their projects.

Let’s dive in!

## Step 1: Create Your Code

The first step is to create the code you want to package and share. You’ll likely already have a module or library in mind that you'd like to distribute, but let’s create a simple example for this blog.

For this example, let's create a simple module called `SimpleMath` with a basic function that adds two numbers together.

1. Create a new Elixir project:

   ```bash
   $ mix new simple_math
   ```

2. Navigate to the project directory:

   ```bash
   $ cd simple_math
   ```

3. Open the `lib/simple_math.ex` file and modify it to look like this:

   ```elixir
   defmodule SimpleMath do
     @moduledoc """
     A simple math library with basic functions.
     """

     @doc """
     Adds two numbers together.

     ## Examples

         iex> SimpleMath.add(2, 3)
         5

     """
     def add(a, b) do
       a + b
     end
   end
   ```

Now that you’ve written your code, it’s time to set it up as a package.

## Step 2: Set It Up as a Package in `mix.exs`

To prepare your code for publishing, you need to update the `mix.exs` file to include important information about your package, like its name, version, description, and dependencies.

Open your `mix.exs` file and modify the `def project` function as follows:

```elixir
def project do
  [
    app: :simple_math,
    version: "0.1.0",
    elixir: "~> 1.12",
    start_permanent: Mix.env() == :prod,
    deps: deps(),
    description: "A simple math library for basic arithmetic operations.",
    package: package(),
    source_url: "https://github.com/your_username/simple_math"
  ]
end

defp package do
  [
    maintainers: ["Your Name"],
    licenses: ["MIT"],
    links: %{"GitHub" => "https://github.com/your_username/simple_math"}
  ]
end
```

Make sure to replace `"Your Name"` and the GitHub URL with your own details. This information will be displayed on the Hex package page.

You also need to ensure you have a valid license file. For example, if you're using the MIT license, create a `LICENSE.md` file with the text of the MIT license. 

## Step 3: Install Hex on Your Local Machine

Hex is the package manager for Elixir, and you'll need to install it locally if you haven't already. To do this, run the following command:

```bash
$ mix local.hex
```

This will install Hex so you can interact with the Hex.pm service to register an account and publish your packages.

## Step 4: Create a Hex Account

If you haven’t registered on [Hex.pm](https://hex.pm), you need to create an account. This is done directly from your terminal with the following command:

```bash
$ mix hex.user register
```

You’ll be prompted to provide your username, email, and password. Here's an example of what the process looks like:

```bash
$ mix hex.user register
Username: johndoe
Email: john.doe@example.com
Password:
Password (confirm):
Registering...
Generating API key...
```

After registration, you'll receive a confirmation email. Make sure to click the link to verify your email before proceeding.

## Step 5: Publish Your Package

Once your code is ready, and your Hex account is confirmed, you can publish your package to Hex.pm. Run the following command:

```bash
$ mix hex.publish
```

You’ll be prompted to review the package information. If everything looks correct, confirm the publish process. After that, your package will be live on Hex.pm!

## Step 6: Publish Your Documentation

Hex allows you to publish online documentation alongside your package, which can be very helpful for users. To do this, make sure you’ve written appropriate documentation in your code (for example, using `@moduledoc` and `@doc` attributes), and then run:

```bash
$ mix hex.publish docs
```

This will generate and publish the HTML documentation for your package, making it accessible on Hex’s package page.

## Example Package for Readers to Follow

If you'd like a simple dependency to practice with, the example we used in this blog (`SimpleMath`) is perfect. It has just one function to add numbers together. You can expand on this by adding other basic math functions like `subtract/2`, `multiply/2`, or `divide/2`.

Here’s the code for the complete module:

```elixir
defmodule SimpleMath do
  @moduledoc """
  A simple math library with basic functions.
  """

  @doc """
  Adds two numbers together.

  ## Examples

      iex> SimpleMath.add(2, 3)
      5

  """
  def add(a, b), do: a + b
end
```

And remember, you can find this package on [Hex.pm](https://hex.pm) under the name `simple_math`.

## Conclusion

Congratulations! You’ve successfully created, packaged, and published an Elixir dependency to Hex. By following these steps, you can now share your code with the world and contribute to the vibrant Elixir community. 

If you’re looking for inspiration, check out the Hex.pm website to see the thousands of other libraries already published. It’s a great way to get ideas for what you might want to build next.
