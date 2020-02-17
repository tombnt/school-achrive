# Binary Search Tree

```java

public class BinarySearchTree<ContentType extends ComparableContent<ContentType>> {

	private ContentType wurzel;
	private BinarySearchTree<ContentType> ltb, rtb;

	public BinarySearchTree() {
	}

	public List<ContentType> getSortedList() {
		List<ContentType> l = new List();
		inOrder(l);
		return l;
	}

	private void inOrder(List<ContentType> l) {
		if (!ltb.isEmpty()) {
			this.getLeftTree().inOrder(l);
		}
		l.append(wurzel);
		if (!rtb.isEmpty()) {
			rtb.inOrder(l);
		}
	}

	public List<ContentType> getPreList() {
		List<ContentType> l = new List();
		preOrder(l);
		return l;
	}

	private void preOrder(List<ContentType> l) {
		l.append(wurzel);
		if (!ltb.isEmpty()) {
			this.getLeftTree().preOrder(l);
		}

		if (!rtb.isEmpty()) {
			rtb.preOrder(l);
		}
	}

	public List<ContentType> getPostList() {
		List<ContentType> l = new List();
		postOrder(l);
		return l;
	}

	private void postOrder(List<ContentType> l) {
		if (!ltb.isEmpty()) {
			this.getLeftTree().postOrder(l);
		}

		if (!rtb.isEmpty()) {
			rtb.postOrder(l);
		}
		l.append(wurzel);
	}

	private boolean isLeaf() {
		if (ltb.isEmpty() && rtb.isEmpty()) {
			return true;
		} else {
			return false;
		}
	}

	public boolean isEmpty() {
		if (wurzel == null) {
			return true;
		} else {
			return false;
		}
	}

	public void insert(ContentType pContent) {
		if (pContent != null) {
			if (this.search(pContent) == null) {

				if (this.isEmpty()) {
					wurzel = pContent;
					ltb = new BinarySearchTree<ContentType>();
					rtb = new BinarySearchTree<ContentType>();
				} else {
					if (pContent.isLess(wurzel)) {
						ltb.insert(pContent);
					} else {
						rtb.insert(pContent);
					}
				}
			}
		}
	}

	public BinarySearchTree<ContentType> getLeftTree() {
		if (ltb.isEmpty()) {
			return null;
		} else {
			return ltb;
		}
	}

	public BinarySearchTree<ContentType> getRightTree() {
		if (rtb.isEmpty()) {
			return null;
		} else {
			return rtb;
		}
	}

	public ContentType search(ContentType pContent) {
		if (pContent == null) {
			return null;
		} else {
			if (this.isEmpty()) {
				return null;
			} else {
				if (pContent.isEqual(wurzel)) {
					return pContent;
				} else {
					if (pContent.isLess(wurzel)) {
						return ltb.search(pContent);
					} else {
						return rtb.search(pContent);
					}
				}
			}
		}
	}

	public void remove(ContentType pContent) {
		if (pContent != null && this.search(pContent) == pContent) {
			if (pContent.isEqual(wurzel)) {
				if (this.isLeaf()) {
					wurzel = null;
					rtb = null;
					ltb = null;
				} else {
					IndexList<ContentType> litB = new IndexList();
					preOrder(litB);
					IndexList<ContentType> retB = new IndexList();
					preOrder(retB);
					wurzel = null;
					rtb = null;
					ltb = null;
					if (litB.length() >= retB.length()) {
						litB.toFirst();
						retB.toFirst();
						while (litB.hasAccess() || retB.hasAccess()) {
							if (litB.hasAccess()) {
								this.insert(litB.getContent());
								litB.next();
							}
							if (retB.hasAccess()) {
								this.insert(retB.getContent());
								retB.next();
							}
						}
					} else {
						litB.toFirst();
						retB.toFirst();
						while (litB.hasAccess() || retB.hasAccess()) {
							if (retB.hasAccess()) {
								this.insert(retB.getContent());
								retB.next();
							}
							if (litB.hasAccess()) {
								this.insert(litB.getContent());
								litB.next();
							}
						}
					}
				}
			} else {
				if (pContent.isLess(wurzel)) {
					ltb.remove(pContent);
				} else {
					rtb.remove(pContent);
  				}
		 	}

		}
	}

	public ContentType getContent() {
        return wurzel;

	}
}

```
