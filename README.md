# homework_algorithm
算法设计与分析作业
github使用基础：https://blog.csdn.net/black_sneak/article/details/139600633

作业1：
问题9：
①  伪代码
function QuickSort(A, p, r)
    if p < r
        // 使用 BB 选择数组中位数附近的元素作为基准
        mid = (p + r) // 2
        pivotIndex = BB(A, p, r, mid)
        
        // Partition: 将数组根据基准元素分成两部分
        q = Partition(A, p, r, pivotIndex)
        
        // 递归地对左半部分和右半部分排序
        QuickSort(A, p, q - 1)
        QuickSort(A, q + 1, r)
    end if
end function

// Partition 算法，返回基准元素的位置
function Partition(A, p, r, pivotIndex)
    pivotValue = A[pivotIndex]
    swap(A[pivotIndex], A[r])  // 将基准元素放到数组的末尾
    i = p - 1
    for j = p to r - 1
        if A[j] <= pivotValue
            i = i + 1
            swap(A[i], A[j])
        end if
    end for
    swap(A[i + 1], A[r])  // 将基准元素放到正确的位置
    return i + 1
end function

// 选择算法 BB (基于 Median of Medians)
function BB(A, p, r, k)
    if r - p + 1 <= 5
        return InsertionSort(A, p, r)[k]
    
    // 分组：每5个元素一组
    for i = p to r by 5
        end = min(i + 4, r)
        groupMedian = InsertionSort(A, i, end)[(end - i) // 2]
        swap(A[p + (i - p) // 5], groupMedian)  // 将每组的中位数放到数组前面
    
    // 递归调用：通过选出中位数的中位数
    mid = (p + r) // 2
    return BB(A, p, p + (r - p) // 5, mid)  // 选择中位数的中位数
end function

// 插入排序，返回排序后的数组
function InsertionSort(A, p, r)
    for i = p + 1 to r
        key = A[i]
        j = i - 1
        while j >= p and A[j] > key
            A[j + 1] = A[j]
            j = j - 1
        end while
        A[j + 1] = key
    end for
    return A
end function
分析：
