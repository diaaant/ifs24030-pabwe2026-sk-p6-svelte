<script>
  import { useInput } from "../../../hooks/useInput.js";
  import { register } from "../states/authStore.js";
  import { navigate, link } from "../../../router.js";
  import { handleResult } from "../../../helpers/toolsHelper.js";

  const name = useInput();
  const email = useInput();
  const password = useInput();
  const nameValue = name.value;
  const emailValue = email.value;
  const passwordValue = password.value;
  let loading = $state(false);

  async function submit(event) {
    event.preventDefault();
    loading = true;
    const res = await register($nameValue, $emailValue, $passwordValue);
    loading = false;
    await handleResult(res, () => navigate("/auth/login"));
  }
</script>

<form onsubmit={submit} class="space-y-4" data-testid="register-form">
  <h2 class="text-lg font-bold">Daftar</h2>
  <div>
    <label for="name" class="block text-sm font-medium mb-1">Nama</label>
    <input id="name" type="text" required value={$nameValue} oninput={name.onChange}
      class="w-full rounded-lg border border-slate-300 px-3 py-2 text-sm" />
  </div>
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
    {loading ? "Memproses..." : "Daftar"}
  </button>
  <p class="text-sm text-center text-slate-500">
    Sudah punya akun? <a href="/auth/login" onclick={link} class="text-indigo-600 font-semibold">Masuk</a>
  </p>
</form>
