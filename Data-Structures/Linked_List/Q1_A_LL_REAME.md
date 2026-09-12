```c
int insertSortedLL(LinkedList *ll, int item)
{
	/* add your code here */

	//struct _listnode newNode = {item, *next = NULL}

	ListNode *newNode = malloc(sizeof(ListNode)); //힙 영역으로 메모리 공간 할당
	newNode->item = item;
	newNode->next = NULL;

	//리스트가 비었을 때
	if (ll->head == NULL) {
		ll->head = newNode;
		return;
	}
		


	//맨 앞에 삽입할 때
	if (ll->head->item > item) {
		ll->head = newNode
		newNode->next = ll->head
	} => 이렇게 하면 안되는 이유: head를 뉴노드로 먼저 교체해버리면 기존 헤드가 사라진다. 따라서 순서를 반대로 해야한다.


	
	// 중간에 삽입할 때
	ListNode* prevNode = NULL;
	ListNode* curNode = ll->head;

	while (curNode != NULL) {
		if (curNode->item > item) {
			newNode->next = curNode;
			prevNode->next = newNode;

			break;
		}

		prevNode = curNode;
		curNode = curNode->next;

	}


	//맨 뒤에 삽입할 때
	if (curNode->next == NULL) {
		curNode->next = newNode;
	} => 이렇게 하면 안되는 이유: while문이 curNode가 NULL인 채로 끝나기 때문이다. 따라서 if문 안에 조건을 curNode == NULL로 잡는다. 또한 curNode가 null인데 다음 노드를 넣을 수 없으므로
    마지막 노드를 가리키는 prevNode->next에 newNode를 넣는다.



	// for (i = 0; i < ll.size; i++) {
	// 	curNode = &ll[i];
	// 	curVal = curNode.item;

	// 	if (curVal > item) {
	// 		prevNode = &ll[i - 1]
	// 		prevNode.next = &newNode
	// 		newNode.next = &curNode
	// 		break;
	// 	}
	// }

제일 중요한 건 ll->size를 증가시켜야 한다는 것이다.
노드가 삽입되면 링크드 리스트의 크기도 같이 늘어나야 한다.
그렇게 안 하면 LinkedList가 가지고 있는 "노드가 몇 개 있는지"라는 정보가 틀리게 된다.

```c
findNode
if (ll == NULL || index < 0 || index >= ll->size)
    return NULL;
```

실제 리스트가 4개인데 size = 3이면:

index 0 → 가능
index 1 → 가능
index 2 → 가능
index 3 → ❌ NULL

즉 실제로 존재하는 4번째 노드를 못 찾게 됨.


insertNode
if (ll == NULL || index < 0 || index > ll->size + 1)
    return -1;

여기도 size를 기준으로 삽입 가능한 위치를 판단해.

removeNode
if (ll == NULL || index < 0 || index >= ll->size)
    return -1;

마찬가지로 실제 노드는 있는데 size가 작으면 삭제할 수 없게 돼.
```
}



