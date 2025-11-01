comparisons = 0
assignments = 0

def swap(arr, i, j):
    global assignments
    arr[i], arr[j] = arr[j], arr[i]
    assignments += 3

def sink(arr, i, n):
    global comparisons, assignments
    k = i
    while True:
        j = 2 * k + 1
        comparisons += 1
        if j >= n:
            break
        comparisons += 1
        if j + 1 < n and arr[j + 1] > arr[j]:
            j += 1
            assignments += 1
        comparisons += 1
        if arr[k] >= arr[j]:
            break
        swap(arr, k, j)
        k = j
        assignments += 1

def heapsort(arr):
    global comparisons, assignments
    n = len(arr)
    print(f"Початковий масив: {arr}\n")

    print("--- Фаза 1: Побудова максимальної купи ---")
    for i in range(n // 2 - 1, -1, -1):
        print(f"Занурюємо елемент з індексу {i}: {arr[i]}")
        sink(arr, i, n)

    print(f"\nМасив після побудови купи: {arr}\n")

    print("--- Фаза 2: Сортування ---")
    for i in range(n - 1, 0, -1):
        print(f"Міняємо місцями корінь ({arr[0]}) та останній елемент ({arr[i]})")
        swap(arr, 0, i)
        n -= 1
        print(f"Розмір купи зменшився до {n}. Відновлюємо властивості купи.")
        sink(arr, 0, n)
        print(f"Масив на поточному кроці: {arr}\n")

    return arr

A = [46, 11, 49, 78, 77, 4, 62, 8, 69]
sorted_A = heapsort(A)
print(f"Відсортований масив: {sorted_A}")
print(f"Загальна кількість порівнянь: {comparisons}")
print(f"Загальна кількість присвоєнь: {assignments}")
