<script>
  import { useInput } from "../../../hooks/useInput.js";
  import { login } from "../states/authStore.js";
  import { navigate, link } from "../../../router.js";
  import { isSuccess } from "../../../helpers/apiHelper.js";
  import { showErrorDialog } from "../../../helpers/toolsHelper.js";

  const email = useInput();
  const password = useInput();
  const emailValue = email.value;
  const passwordValue = password.value;
  let loading = $state(false);

  async function submit(event) {
    event.preventDefault();
    loading = true;
    const res = await login($emailValue, $passwordValue);
    loading = false;
    if (isSuccess(res)) navigate("/");
    else await showErrorDialog(res.message);
  }
</script>

<form onsubmit={submit} class="space-y-4" data-testid="login-form">
  <h2 class="text-lg font-bold">Masuk</h2>
  <div>
    <label for="email" class="block text-sm font-medium mb-1">Email</label>
    <input id="email" type="email" required value={$emailValue} oninput={email.onChange}
      class="w-full rounded-lg border border-slate-300 px-3 py-2 text-sm" />
  </div>
  <div>
    <label for="password" class="block text-sm font-medium mb-1">Kata sandi</label>
    <input id="password" type="password" required value={$passwordValue} oninput={password.onChange}
      class="w-full rounded-lg border border-slate-300 px-3 py-2 text-sm" />
  </div>
  <button type="submit" disabled={loading}
    class="w-full rounded-lg bg-indigo-600 text-white py-2 text-sm font-semibold disabled:opacity-60">
    {loading ? "Memproses..." : "Masuk"}
  </button>
  <p class="text-sm text-center text-slate-500">
    Belum punya akun? <a href="/auth/register" onclick={link} class="text-indigo-600 font-semibold">Daftar</a>
  </p>
</form>
