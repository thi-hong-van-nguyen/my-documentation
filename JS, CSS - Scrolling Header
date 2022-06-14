# Make the Header black when scroll down
```
function Nav() {
	const [show, handleShow] = useState(false);
	useEffect(() => {
		window.addEventListener("scroll", () => {
			if (window.scrollY > 100) {
				handleShow(true);
			} else {
				handleShow(false);
			}
		});

		return () => {
			window.removeEventListener("scroll", () => {});
		};
	}, []);

	return (
		<div className={`nav ${show && "nav__black"}`}>
	    HEADER
		</div>
	);
}
```

### CSS file:
```
.nav {
	position: fixed;
	top: 0;
	display: flex;
	justify-content: space-between;
	padding: 20px;
	height: 30px;
	width: 100%;
	z-index: 1;

	transition-timing-function: ease-in;
	transition: all 0.5s;
}

.nav__black {
	background: #000;
}
```
